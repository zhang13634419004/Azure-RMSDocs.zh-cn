---
title: 概念 - 使用 Microsoft 信息保护 SDK 生成审核事件
description: 本文将帮助你了解如何使用 Microsoft 信息保护 SDK 进行计算。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 6bf4bc78d6008354275abacddf8f37e42dce1650
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555783"
---
# <a name="compute-an-action"></a>计算操作

如先前所述，策略 API 的主要功能是：

- 列出可用标签
- 根据当前状态和所需状态返回应执行的一组操作

该过程的最后一步是向 `ComputeActions()` 函数提供标签标识符和（可选）现有标签的元数据。

可以在 GitHub 上找到本文的示例代码。

- [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>计算新标签的操作

可以通过使用[executionstate&](concept-handler-policy-executionstate-cpp.md)中定义的 `ExecutionStateImpl`，为新标签计算 `mip::Actions`。

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Resolve desired label id to mip::Label and set in ExecutionStateOptions.
options.newLabel = mEngine->GetLabelById(newLabelId);

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions.
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

只编写作为 `actions` 一部分返回的 `mip::MetadataActions` 会显示：

```cpp
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled : true
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate : 2018-10-23T20:39:06-0800
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method : Standard
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name : Contoso FTEs (C)
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId : 2266fbe8-a0d9-44e8-bad8-00008f2a0915
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits : 3
```

`PolicyHandler` 计算操作并返回 `mip::Action` 的 `std::vector`。 应用开发人员可将此元数据应用于文件或数据。

> [!NOTE]
> 上面的示例仅显示 `mip::MetadataAction` 输出。 有关显示其他操作类型的示例，请查看[策略 API 下载](https://aka.ms/mipsdkbins)的示例包。

## <a name="compute-actions-with-an-existing-label"></a>使用现有标签计算操作

使用策略 API 时，应用程序由应用程序从内容中读取元数据。 此元数据作为 `mip::ExecutionState` 的一部分提供给 API。 `ComputeActions()` 可以处理比将新标签应用于未标记的文档更为复杂的操作。 下面的示例演示如何将标签从更敏感的标签降级为不太敏感的标签。 此过程通过读取逗号分隔的元数据字符串来模拟，并通过 `mip::ExecutionState`向 API 提供。

> [!NOTE]
> 该示例使用名为 `SplitString()` 的实用程序函数。 可在[此处](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/utils.cpp)找到示例

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and resolve newLabelId to mip::Label
sample::policy::ExecutionStateOptions options;
options.newLabel = mEngine->GetLabelById(newLabelId);

// Split metadata string by commas, store in vector.
vector<string> metadataPairs = sample::utils::SplitString(metadata, ','); 

// Iterate through each string, splitting by the pipe.
// Add each key/value pair to ExecutionStateOptions metadata.
for (const string& metadataPair : metadataPairs) {
    vector<string> keyValue = sample::utils::SplitString(metadataPair, '|');
    options.metadata[keyValue[0]] = keyValue[1];
}

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

上面的示例可能会导致多个操作。 这些操作取决于作为输入提供的标签和标签配置。 至少，结果将是一个包含要通过 `GetMetadataToRemove()` 删除的数据以及要通过 `GetMetadataToAdd()` 添加的数据的 `mip::MetadataAction`。

```
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Enabled : true
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SetDate : 2018-10-23T23:59:41-0800
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Method : Standard
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Name : General
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ActionId : 447a996b-28ea-482c-b0b5-000075bd4bb3
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ContentBits : 7
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId
```

## <a name="next-steps"></a>后续步骤

- 了解如何将[审核事件传递到 Azure 信息保护分析](concept-handler-policy-auditing-cpp.md)
- [从 GitHub 下载策略 Api 示例，并试用策略 api](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)

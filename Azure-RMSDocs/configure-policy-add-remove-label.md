---
title: 向 Azure 信息保护策略添加标签或从中删除标签 - AIP
description: 向所有用户的全局策略或子集用户的作用域内策略添加 Azure 信息保护标签，或从中删除标签。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: bf0567efc0d8ae8c65667f7b65cafbdbd32f83aa
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047722"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>向 Azure 信息保护策略添加标签或从中删除标签

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

创建 Azure 信息保护标签后，可以将其添加到策略，以便它可供用户使用。 如果标签面向所有用户，则将标签添加到全局策略。 如果标签面向所有子集用户，则将标签添加到作用域内策略。 只能将标签添加到一个策略。 

若要添加子标签，其父标签必须位于同一策略中，或位于全局策略中。 添加子标签时，不会继承主标签中的设置。 对于在策略中分配了子标签的用户，仅支持主标签作为名称和颜色的显示容器。 在此情况下，不支持将主标签中的其他配置设置用于视觉标记、保护和条件。 尽管仍然可以配置它们，但是仅支持将主标签中的这些设置用于策略中具有主标签但没有子标签的用户。

对于已存在于一个策略中的标签，可以从策略中将其删除。 此操作不会删除标签。 仍可以在另一个策略中使用。

如果尚未创建标签，请参阅[如何为 Azure 信息保护创建新标签](configure-policy-new-label.md)。

如果需要创建作用域内策略，以便将标签应用到子集用户，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)。

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>若要向策略添加标签或从中删除标签

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”**** 窗格。
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”**** 并选择“Azure 信息保护”****。

2. 从 "**分类**  >  **策略**" 菜单选项：在 " **Azure 信息保护**  -  **策略**" 窗格中，如果要添加或删除的标签适用于所有用户，请选择 "**全局**"。

    如果要添加或删除的标签适用于子集用户，请改为选择作用域内策略。

3. 在 "**策略**" 窗格中，选择 "**添加或删除标签**"。

4. 在 "**策略：添加或删除标签**" 窗格中，将显示 "所有标签" 复选框（如果已在策略中）以及相应的策略名称（在 "**策略**" 列中）。
     
    子标签显示为缩进。 在作用域内策略中，从全局策略继承的标签显示为不可用。
    
    执行下列一项或多项操作，然后单击“确定”****：
    
    - 若要添加标签，请选中，将添加所选的复选框。
    
    - 若要删除标签，请清除其复选框。
  
5. 单击“**保存**”以保存更改。
   
    更改将会自动提供给用户和服务。 不再提供单独发布选项。


## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。

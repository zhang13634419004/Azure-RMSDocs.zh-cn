---
title: 快速入门 - 使用 C++ MIP SDK 列出 Microsoft 信息保护 (MIP) 租户中的敏感度标签
description: 一个演示如何使用 Microsoft 信息保护 C++ SDK 列出租户中的敏感度标签的快速入门。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 07782b754c63b4289bf5630eb41b6885b30c7c78
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82971602"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>快速入门：列出敏感度标签 (C++)

本快速入门演示如何使用 MIP 文件 API 列出为组织配置的敏感度标签。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：客户端应用程序初始化 (C++)](quick-app-initialization-cpp.md)，生成 Visual Studio 初学者解决方案。 此“列出敏感度标签”快速入门需依赖前者来正确创建初学者解决方案。
- 可选：查看[分类标签](concept-classification-labels.md)概念。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>添加用于列出敏感度标签的逻辑

使用文件引擎对象添加用于列出组织敏感度标签的逻辑。

1. 打开在前面的“快速入门：客户端应用程序初始化 (C++)”一文中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 在文件顶部附近的 `using mip::FileEngine;` 后面添加以下 `using` 指令：

   ```cpp
   using std::endl;
   ```

4. 在 `main()` 正文的末尾，在最后一个 `catch` 块的右大括号 `}` 下面并在 `return 0;` 上面（在上一快速入门中离开的位置）插入以下代码：

   ```cpp
   // List sensitivity labels
   cout << "\nSensitivity labels for your organization:\n";
   auto labels = engine->ListSensitivityLabels();
   for (const auto& label : labels)
   {
      cout << label->GetName() << " : " << label->GetId() << endl;

      for (const auto& child : label->GetChildren())
      {
        cout << "->  " << child->GetName() << " : " << child->GetId() << endl;
      }
   }
   system("pause");
   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>创建 PowerShell 脚本以生成访问令牌

在 `AuthDelegateImpl::AcquireOAuth2Token` 实现中按照 SDK 的要求使用以下 PowerShell 脚本生成访问令牌。 该脚本使用先前在“MIP SDK 安装和配置”中安装的 ADAL.PS 模块中的 `Get-ADALToken` cmdlet。

1. 创建 PowerShell 脚本文件（.ps1 扩展名），并将以下脚本复制/粘贴到该文件中：

   - `$authority` 和 `$resourceUrl` 稍后会在下一部分中更新。
   - 更新 `$appId` 和 `$redirectUri`，以匹配在 Azure AD 应用注册中指定的值。

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. 保存该脚本文件，以便稍后按照客户端应用程序的要求运行它。

## <a name="build-and-test-the-application"></a>生成和测试应用程序

最后，生成和测试客户端应用程序。

1. 使用 F6（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireOAuth2Token()` 方法时，应用程序都会提示输入访问令牌。 如果多次提示并且请求的值相同，则可以重用以前生成的令牌：

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token:
   ```

3. 要生成用于在提示中输入的访问令牌，请返回 PowerShell 脚本并执行以下操作：

   - 更新 `$authority` 和 `$resourceUrl` 变量。 它们必须与在步骤 2 的控制台输出中指定的值匹配。 这些值由 MIP SDK 在 `AcquireOAuth2Token()` 的 `challenge` 参数中提供：
     - `$authority` 应为 `https://login.windows.net/common/oauth2/authorize`
     - `$resourceUrl` 应为 `https://syncservice.o365syncservice.com/` 或 `https://aadrm.com`
   - 运行 PowerShell 脚本。 `Get-ADALToken` cmdlet 会触发类似于以下示例的 Azure AD 身份验证提示。 指定在步骤 2 的控制台输出中提供的同一帐户。 成功登录后，访问令牌将被放置在剪贴板上。

     [![Visual Studio 获取令牌登录](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - 可能还需同意应用程序在登录帐户下运行时访问 MIP API。 如果未事先同意 Azure AD 应用程序注册（如“MIP SDK 安装和配置”中所述），或者使用其他租户（而非应用程序注册所在的租户）中的帐户登录，就会出现这种情况。 只需单击“接受”即可记录你的同意。

     [![Visual Studio 同意](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. 将访问令牌粘贴到步骤 #2 的提示符中后，控制台输出应显示敏感度标签，类似于以下示例：

   ```console
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z

   Press any key to continue . . .
   ```

   > [!NOTE]
   > 复制并保存一个或多个敏感度标签的 ID（例如，`f42a3342-8706-4288-bd31-ebb85995028z`），因为你将在下一个快速入门中使用它。

## <a name="troubleshooting"></a>疑难解答

### <a name="problems-during-execution-of-powershell-script"></a>执行 PowerShell 脚本时出现的问题

| “摘要” | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 应用程序注册或 PowerShell 脚本中的重定向 URI 不正确 (AADSTS50011) |AADSTS50011:请求中指定的回复 URL 与为应用程序配置的回复 URL 不匹配: "ac6348d6-0d2f-4786-af33-07ad46e69bfc"。 | 通过完成以下步骤之一，验证正在使用的重定向 URI：<br><br><li>更新 Azure AD 应用程序配置中的重定向 URI，以匹配 PowerShell 脚本。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md#register-a-client-application-with-azure-active-directory)，验证是否已正确配置重定向 URI 属性。<br><li>更新 PowerShell 脚本中的 `redirectUri` 变量，以匹配应用程序注册。 |
| 登录帐户不正确 (AADSTS50020) | AADSTS50020:来自标识提供者“https://sts.windows.net/72f988bl-86f1-41af-91ab-2d7cd011db47/ ”的用户帐户“user@domain.com”不存在于租户 "Organization name" 中，且无法访问该租户中的应用程序 "0edbblll-8773-44de-b87c-b8c6276d41eb"。 | 完成以下步骤之一：<br><br><li>重新运行 PowerShell 脚本，但务必使用 Azure AD 应用程序注册所在的同一租户中的帐户。<br><li>如果登录帐户是正确的，则 PowerShell 主机会话可能已在其他帐户下进行身份验证。 在这种情况下，请在退出脚本主机后重新打开，然后再次尝试运行它。<br><li>如果将此快速入门用于 Web 应用（而非本机应用），并且需要使用其他租户中的帐户登录，请确保为 Azure AD 应用程序注册启用多租户使用。 可以使用应用程序注册中的“编辑清单”功能进行验证，并确保它指定 `"availableToOtherTenants": true,`。 |
| 应用程序注册中的权限不正确 (AADSTS65005) | *AADSTS65005:资源无效。客户端已请求访问某个资源，但该资源未在客户端应用程序注册中的所需权限中列出。客户端应用 ID:0edbblll-8773-44de-b87c-b8c6276d41eb。来自请求的资源值: https://syncservice.o365syncservice.com/ 。资源应用 ID:870c4f2e-85b6-4d43-bdda-6ed9a579b725。来自应用注册的有效资源列表：00000002-0000-0000-c000-000000000000。* | 更新 Azure AD 应用程序配置中的权限请求。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md#register-a-client-application-with-azure-active-directory)，验证是否在应用程序注册中正确配置了权限请求。 |

### <a name="problems-during-execution-of-c-application"></a>执行 C++ 应用程序时出现的问题

| “摘要” | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 访问令牌不正确 | 发生异常...访问令牌是否不正确/过期?<br><br>API 调用失败: profile_add_engine_asyn 失败原因: [class mip::PolicySyncException] 策略获取失败，请求失败并显示 http 状态代码:401，x-ms-diagnostics: [2000001;reason=“无法解析随请求提交的 OAuth 令牌。”;error_category="invalid_token"]，correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) 已退出，代码为 0。<br><br>按任意键关闭此窗口... | 如果项目成功生成，但出现类似于左侧的输出，则表示 `AcquireOAuth2Token()` 方法中可能包含无效或过期的令牌。 返回到[创建 PowerShell 脚本以生成访问令牌](#create-a-powershell-script-to-generate-access-tokens)并重写访问令牌，再次更新 `AcquireOAuth2Token()`然后重新生成/重新测试。 还可以使用 [jwt.ms](https://jwt.ms/) 单页 Web 应用程序检查并验证令牌及其声明。 |
| 未配置敏感度标签 | n/a | 如果项目成功生成，但在控制台窗口中没有输出，请确保正确配置了组织的敏感度标签。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md)，在“定义标签分类和保护设置”下获取详细信息。  |

## <a name="next-steps"></a>后续步骤

你已经了解如何列出组织的敏感度标签，现在尝试下一个快速入门：

> [!div class="nextstepaction"]
> [设置和获取敏感度标签](quick-file-set-get-label-cpp.md)

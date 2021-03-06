---
title: Windows Phone 安装程序 | Azure RMS
description: Windows Phone 应用程序可以使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 8c36466511749b6148f58c439702c8cd0f252a64
ms.sourcegitcommit: 5390bd1e0e4851b81a59094e80202f0761b7810f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80068512"
---
# <a name="windows-phone-setup"></a>Windows Phone 安装程序

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Windows Phone 应用程序可以使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护（通过使用 Azure Active Directory Rights Management (AAD RM)）。

本主题将指导你完成环境设置过程，以创建自己的新应用。

-   [必备条件](#prerequisites)
-   [配置开发环境](#configuring-your-development-environment)
-   [另请参阅](#see-also)

## <a name="prerequisites"></a>先决条件


开发系统上必须安装以下软件：

-   [Windows 8.1](https://windows.microsoft.com/windows-8/meet) 操作系统。
-   [Windows Phone 8.1 开发工具 (SDK)](https://developer.microsoft.com/windows/downloads/sdk-archive)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) 或更高版本，或 Visual Studio Express 2012，后者包含在 Windows Phone SDK 8.0/8.1 中
-   适用于 Windows Phone 的 MS RMS SDK 4.2 包。 有关详细信息，请参阅[入门](get-started.md)。
-   身份验证库：我们建议使用 [Azure AD 身份验证库](https://msdn.microsoft.com/library/jj573266.aspx)和其他可用的身份验证库。

有关 API 更新、设备和环境信息、发行说明和常见问题 (FAQ) 的信息，请阅读[新增功能](release-notes.md)主题。

请查阅 Windows Phone 开发人员中心处的 [Windows Phone 开发](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx)指南中的信息。

## <a name="configuring-your-development-environment"></a>配置开发环境


-   打开 *Visual Studio*。
-   单击“文件”。 在“文件”菜单上，单击“新建”，然后单击“项目”。
-   在“新建项目”对话框中，依次选择“Visual C”**和“空白应用(Windows Phone)”\#** ，然后单击“确定”。

    ![新建项目](../media/wpsetup-newproj.png)

-   在解决方案资源管理器中，右键单击你的项目，然后选择“添加引用”以打开“添加引用”对话框。

    ![添加引用](../media/wpsetup-addref.png)

-   单击“添加引用”对话框左下角的“浏览”并选择位于将包解压到其中的文件夹中的 *Microsoft.RightsManagment.dll* 文件。
-   **托管应用** - 需要添加此引用才能生成托管应用；请选择 **Windows 8.1**-&gt;**扩展**，并选中“适用于 Windows 的 Windows Visual C++ 运行时包”复选框

    ![添加扩展](../media/wpsetup-refmngr.png)

-   **添加功能** - 你的应用程序将需要“Internet （客户端和服务器）”功能来使用 SDK。 若要将此功能添加到你的应用程序中，请打开项目中的 *Package.appxmanifest* 文件，并导航到“功能”选项卡已进行添加。

你现在已准备就绪，可创建新 Windows Phone 应用。

### <a name="see-also"></a>另請參閱

[入门](get-started.md)

[新增功能](release-notes.md)

[核心概念](core-concepts.md)

[Windows Phone 开发](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx)

[Windows API 参考](https://msdn.microsoft.com/library/dn891914.aspx)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[Windows Phone SDK](https://developer.microsoft.com/windows/downloads/sdk-archive)

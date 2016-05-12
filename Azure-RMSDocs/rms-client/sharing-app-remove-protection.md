---
# required metadata

title: 使用 Rights Management 共享应用程序移除对文件的保护 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 Rights Management 共享应用程序移除对文件的保护
若要移除之前使用 RMS 共享应用程序保护的文件保护（即取消文件保护），请从文件资源管理器中使用“移除保护”选项 **** 。

> [!IMPORTANT]
> 你必须是文件所有者才能移除保护。

## 移除对文件的保护

1.  在文件资源管理器中，右键单击文件（例如 Sample.ptxt），选择“使用 RMS 保护”****，单击“就地保护”****，然后单击“移除保护”****：

    ![](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    系统可能会提示你输入凭据。

注意：如果看不到这些选项，则很可能你的计算机上未安装 RMS 共享应用程序、未安装最新版本，或必须重启计算机才能完成安装。 有关如何安装共享应用程序的详细信息，请参阅[下载和安装 Rights Management 共享应用程序](install-sharing-app.md)。

原始的受保护文件（例如 Sample.ptxt）将会删除，并替换为一个同名但文件扩展名不受保护的文件（例如 Sample.txt）。

## 示例和其他说明
有关如何使用 Rights Management 共享应用程序以及操作说明的示例，请参阅以下 Rights Management 共享应用程序用户指南部分：

-   [使用 RMS 共享应用程序的示例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [要执行什么操作？](sharing-app-user-guide.md##what-do-you-want-to-do-)

## 另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)



<!--HONumber=Apr16_HO3-->


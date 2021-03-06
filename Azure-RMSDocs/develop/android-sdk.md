---
title: Android 安装程序 |Azure RMS
description: Android 应用程序可以使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: ef1306dbcbd4727f4e6c0207e328e7df3da8ed74
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82971891"
---
# <a name="android-setup"></a>Android 安装程序

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Android 应用程序可以通过使用 Azure Active Directory Rights Management (AAD RM)，利用 Microsoft Rights Management SDK 4.2 在其应用中启用集成信息保护。

本主题将指导你完成环境设置过程，以创建自己的新应用。

-   [先决条件](#prerequisites)
-   [可选](#optional)
-   [配置开发环境](#configuring-your-development-environment)
-   [另请参阅](#see-also)

## <a name="prerequisites"></a>先决条件

我们建议在开发系统上安装以下软件：

-   Windows 或 OS X 操作系统，用于运行 [Eclipse](https://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 开发环境。
-   本指南假定你在使用从 Eclipse Juno 4.2 开始的 Eclipse SDK 并使用默认安装。
-   从 Java 1.6 开始的 Java。
-   [Android 开发人员工具 (ADT) 插件](https://developer.android.com/studio/install)。 注意 - 可能会请你重新启动 Eclipse 以完成安装。



-   适用于 Android 的 MS RMS SDK 4.2 包。 有关详细信息，请参阅[入门](get-started.md)。

    此 SDK 可以用于为 Android 4.0.3（API 级别 15）及更高版本进行开发。

-   身份验证库：我们建议使用 [Azure AD 身份验证库 (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)。 但是也可使用其他支持 OAuth 2.0 的身份验证库。

    有关详细信息，请参阅 [ADAL for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

    **注意**  如果你的应用程序将不使用 ADAL 库作为 OAuth 2.0 身份验证库，你应该查看此 Android 指南，[一些 java.security.securerandom](https://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html)。



有关 API 更新、发行说明和常见问题解答 (FAQ) 的信息，请阅读[新增功能](release-notes.md)主题。

## <a name="optional"></a>可选

我们的 UI 库可为不想创建自己的自定义 UI 的开发人员提供用于使用和保护操作的可重用 UI - [适用于 Android 的 UI 库和示例](https://github.com/AzureAD/rms-sdk-ui-for-android)。

## <a name="configuring-your-development-environment"></a>配置开发环境

**注意**  MS RMS SDK 4.2 预览版：在此预览版本中，屏幕截图尚未更新，以显示 pathes 从 com/microsoft/protection 到 com/microsoft/rightsmanagment 的名称更改。 不过文本已进行了更新。


-   打开 Eclipse 开发环境。
-   若要创建新 Android 应用程序项目，请在 **“文件”** 菜单上，单击 **“新建”**，单击 **“项目”**，然后选择 **“Android 应用程序项目”**。

    ![创建新的 Android 应用程序](../media/Android-setup-01c.png)

-   输入应用程序名称。 项目名称和包名称根据应用程序名称进行填充。
-   单击 **“下一步”**，然后选择要用于创建工作区的位置。

    ![输入应用程序名称](../media/Android-setup-02a.jpg)

-   单击 **“下一步”**，然后为应用选择图标。

    ![为应用选择图标](../media/Android-setup-03.png)

-   单击 **“下一步”**，然后选择 **“空白活动”** 以创建活动。

    ![创建活动](../media/Android-setup-04.png)

-   单击 **“下一步”** 并提供活动的名称。 可以将*MainActivity*保留为默认名称，其中布局名称为 "*活动\_主*"。

    ![提供活动的名称](../media/Android-setup-05a.jpg)

-   单击“完成”  。

    ![完成创建](../media/Android-setup-06.jpg)

-   项目以及主活动类 *MainActivity.java* 已创建。

**引用 SDK**

- 导航到已在其中提取*\_adrms android\_sdk*的文件夹。 在“SDK > com > microsoft > rightsmanagement”文件夹中，确保文件 *.classpath*、*.project* 和 *project.properties* 未标记为只读。
- 若要引用 SDK，必须将它导入工作区中。

  在 Eclipse 中，单击 **“文件”**。 在 **“文件”** 菜单上，单击 **“导入”**。 在 **“导入”** 对话框中，选择 **“Android/现有 Android 代码到工作区”**。

  ![将其导入到工作区](../media/Android-setup-07.png)

- 单击“下一步”。  导航以选择在其中提取*\_adrms android\_sdk*的文件夹。 SDK 应作为 **com.microsoft.rightsmanagement** 显示在列表中。

  ![导航到“选择文件夹”](../media/Android-setup-08c.jpg)

- 单击 **“完成”** 时，SDK 项目显示为以前创建的应用程序的同级。

  ![该 SDK 项目将显示为应用程序的同级](../media/Android-setup-09.jpg)

- 右键单击 **“项目”** 图标并查看项目的属性。
- 导航到 **“Android”** 选项卡。
- 单击 **“添加”**，然后从工作区中选择 *com.microsoft.rightsmanagement* 库。

  ![添加库](../media/Android-setup-10b.jpg)

- 单击“确定”。 

  由于 MS RMS SDK 4.2 与 AAD RM 连接，因此应用程序必须被授予**INTERNET**并**\_访问网络\_状态**。 为此，请在项目的根目录中打开 *AndroidManifest.xml* 文件。

  若要添加权限，请单击 **“添加”**，然后选择 **“使用权限”**。

  ![添加权限](../media/Android-setup-11d.jpg)

- 可以通过在文本编辑器视图中查看清单来验证清单步骤。 确保显示以下行：

  ```
  <uses-sdk
       android:minSdkVersion="15"
       android:targetSdkVersion="19"/>
  <uses-permission android:name="android.permission.INTERNET"/>
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
  <uses-permission/>
  ```

**请注意**  ，SDK 使用的*支持 v4*

-   你现在已准备就绪，可创建新 Android 应用。

### <a name="see-also"></a>另请参阅

[入门](get-started.md)

[新增功能](release-notes.md)

[开发人员术语和概念](core-concepts.md)

[Android API 参考](https://msdn.microsoft.com/library/dn758245.aspx)

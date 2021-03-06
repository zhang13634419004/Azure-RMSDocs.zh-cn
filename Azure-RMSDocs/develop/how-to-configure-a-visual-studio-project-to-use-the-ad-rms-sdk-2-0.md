---
title: 配置 Visual Studio | Azure RMS
description: 有关如何配置 Visual Studio 项目以使用 RMS SDK 2.1 的说明。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: d36938daf4dbcbe86331ec6852dfe4ecb04a2959
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68792410"
---
# <a name="configure-visual-studio"></a>配置 Visual Studio

本主题包含有关如何配置 Visual Studio 项目以使用 Rights Management Services SDK 2.1 的说明。

## <a name="prerequisites"></a>必备条件

-   [安装 SDK](install-the-rms-sdk.md)

**说明**

### <a name="step-1-configure-a-visual-studio-project-to-use-rmssdk21"></a>步骤1：配置 Visual Studio 项目以使用 RMS SDK 2。1

这些说明特定于 Microsoft Visual Studio 2010。 如果使用不同版本的 Microsoft Visual Studio，则设置对话框可能略有不同。

这些说明适用于构建本机 32 位应用程序。

1.  将 RMS SDK 2.1 包含目录添加到 Visual Studio 2010 项目。

    在“配置属性”下，选择“VC++ 目录”，并将 RMS SDK 2.1 包含目录 $(MSIPCSDKDIR)\\inc 添加到“包含目录”字段。

    ![配置属性包含目录字段](../media/include_directories.png)

2.  将 RMS SDK 2.1 库目录添加到 Visual Studio 2010 项目。

    在“配置属性”下，选择“VC++ 目录”，并针对你的平台将 RMS SDK 2.1 库目录添加到“库目录”字段。

    -   对于 Win32，使用 **$(MSIPCSDKDIR)\\lib**
    -   对于 x64，使用 **$(MSIPCSDKDIR)\\lib\\x64**

    ![配置属性库目录字段](../media/library_directories.png)

3.  将 RMS SDK 2.1 库文件添加为 Visual Studio 2010 依赖项。

    在“链接器”下，选择“输入”，然后将 RMS SDK 2.1 库文件 Msipc.lib 和 Msipc\_s.lib 添加到“附加依赖项”字段。

    ![链接器库依赖项字段](../media/additional_dependencies.png)

4.  将 RMS SDK 2.1 动态链接库 (DLL) 添加为延迟加载的 DLL。

    在“链接器”下，选择“输入”，并将 RMS SDK 2.1 DLL 文件 Msipc.dll 添加到“延迟加载的 DLL”字段。

    ![链接器延迟加载的库字段](../media/delay_loaded.png)

5.  为生成的二进制文件创建版本信息。

    在 **“解决方案资源管理器”** 下，选择 **“资源文件”** ，然后将二进制文件名称添加到 **“OriginalFileName”** 字段。

    ![解决方案资源管理器资源文件字段](../media/original_file_name.png)

## <a name="related-topics"></a>相关主题

* [安装 SDK](install-the-rms-sdk.md)

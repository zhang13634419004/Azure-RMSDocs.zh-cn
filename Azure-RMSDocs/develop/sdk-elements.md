---
title: 开发环境文件 | Azure RMS
description: 本主题展示开发环境文件和它们在计算机上的相对安装位置。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 3c9bca4e474306d3e73df8d9d41a7c4ef9c6e5e2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68790818"
---
# <a name="development-environment-files"></a>开发环境文件

本主题展示开发环境文件和它们在计算机上的相对安装位置。

Rights Management Services SDK 2.1 包括安装在计算机上默认位置或指定位置的以下文件：%MsipcSDKDir%。

|文件|路径|描述|
|----|----|-----------|
|ReadMe.htm| \ | 包含 RMS 帮助和[发行说明](release-notes-rtm.md)的链接。|
|Isvtier5appsigningprivkey.dat|\bin|包含一个私钥，用于生成支持 RMS 的应用程序开发期间要使用的清单。|
|Isvtier5appsigningpubkey.dat|\bin|包含用于生成清单以在 RMS 启用的引用程序的开发期间使用的公匙。|
|Isvtier5appsignsdk_client.xml|\bin|用于生成清单以在 RMS 启用的引用程序的开发期间使用。|
|YourAppName.isv.mcf|\bin|一个样板清单配置文件，可用于在支持 RMS 的应用程序开发期间生成清单。|
|Ipcsecproc_isv.dll|\bin\x86|在 ISV 层次结构中进行操作时由 Active Directory Rights Management Services Client 2.1 在内部用于 x86 应用程序的 DLL。|
|Ipcsecproc_ssp_isv.dll|\bin\x86|在 ISV 层次结构中进行操作时由 AD RMS 2.1 在内部用于 x86 应用程序的 DLL。|
|Ipcsecproc_isv.dll|\bin\x64|由 AD RMS Client 2.1 在 ISV 层次结构中进行操作时内部用于 x64 应用程序的 DLL。|
|Ipcsecproc_ssp_isv.dll|\bin\x64|由 AD RMS Client 2.1 在 ISV 层次结构中进行操作时内部用于 x64 应用程序的 DLL。|
|Msipc.h|\inc|主要包括用于 RMS SDK 2.1 的文件。|
|Ipcprot.h|\inc|包含由 RMS SDK 2.1 导出的公共接口。|
|Ipcbase.h|\inc|包含由 RMS SDK 2.1 导出的基本类型和帮助程序函数。|
|Ipcerror.h|\inc|包含由 RMS SDK 2.1 导出的公共错误代码。|
|Ipcfile.h|\inc|包含由 RMS SDK 2.1 导出的文件 API 接口。|
|Msipc.lib|\lib|使用 RMS SDK 2.1 生成 x86 应用程序时要链接的库。|
|Msipc_s.lib|\lib|为 x86 应用程序提供 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) 的入口点。|
|Msipc.lib|\lib\x64|当使用 RMS SDK 2.1 生成 x64 应用程序时要与之链接的库。|
|Msipc_s.lib|\lib\x64|为 x64 应用程序提供 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) 的入口点。|
|Genmanifest.exe|\tools|生成清单以在 RMS 启用的引用程序的开发期间使用。|

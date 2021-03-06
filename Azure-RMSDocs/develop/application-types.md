---
title: 应用程序类型 | Azure RMS
description: 本主题介绍可以选择创建为启用权限形式的应用程序类型。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 06a92e4b2da227ede08249479554d12526fe2432
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68791288"
---
# <a name="application-types"></a>应用程序类型


本主题介绍可以选择创建为启用权限形式的应用程序类型。

Rights Management Services SDK 2.1 当前支持以下应用程序类型

## <a name="simple-applications"></a>简单应用程序

简单应用程序可以是为加密提供的文件而构建的命令行工具。 有关启用权限的简单应用程序的示例，请参阅[开发应用程序](developing-your-application.md)中所述的 *IPCHelloWorld* 实现。

### <a name="server-mode-applications"></a>服务器模式应用程序

*服务器模式* 面向使用、保护或处理受 RMS 保护的内容的非交互式应用程序。 一个示例是 *数据丢失防护* 应用程序，该应用程序在文件服务器上作为服务运行，会自动保护敏感文档。 有关此应用程序类型的示例，请参阅 [IpcDlp 示例](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcDlpApp)。

如果应用程序使用 *服务器模式*，则它应以无提示方式向 RMS 服务器进行身份验证。 与“客户端模式”不同，RMS SDK 2.1 在未能以无提示方式进行身份验证时不会打开凭据提示。 此外，在 *服务器模式* 下运行时，无需应用程序清单。

有关设置 API 安全模式的详细信息，请参阅 [设置 API 安全模式](setting-the-api-security-mode-api-mode.md)。

### <a name="rich-client-applications"></a>富客户端应用程序

富客户端应用程序允许用户通过图形用户界面 (GUI) 查看和操作数据。 通常，在此 GUI 中呈现的数据具有高价值，对被盗或意外公开十分敏感。 信息保护支持通常可增强现有方案，但不是开发应用程序的主要动机。

将 RMS SDK 2.1 与富客户端应用程序一起使用可帮助：

-   确保此数据始终进行加密。

-   防止用户将数据提取为不受保护的格式（例如，防止使用剪贴板复制和粘贴）。

Microsoft 记事本是简单的富客户端应用程序。 Microsoft Office 是更加复杂的富客户端应用程序。

有关保护应用程序的详细信息，请参阅 [了解使用限制](understanding-usage-restrictions.md)。

## <a name="related-topics"></a>相关主题

- [IpcDlp 示例](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
- [开发应用程序](developing-your-application.md)
- [设置 API 安全模式](setting-the-api-security-mode-api-mode.md)
- [了解使用限制](understanding-usage-restrictions.md)

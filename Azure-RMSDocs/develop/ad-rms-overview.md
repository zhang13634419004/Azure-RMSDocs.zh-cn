---
title: 概述 - RMS SDK 2.1 | Azure RMS
description: Rights Management Services (RMS) 是一种信息保护技术，可帮助保护数字信息免遭未经授权的使用。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 6f36ef984a6d6d10ce06ae690c98153524a7d301
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68791471"
---
# <a name="overview"></a>“概述”

Rights Management Services SDK 2.1 是一种信息保护技术，可帮助保护数字信息免遭未经授权的使用。 通过启用权限的应用程序，内容所有者将能够定义可以对内容进行打开、修改、打印、转发或执行其他操作的人员。

AD RMS 由 [服务器](ad-rms-server.md) 和 [客户端](ad-rms-client.md) 组件组成。 此服务器在 Azure 或 Windows Server 上运行，由多个 Web 服务组成。

[客户端](ad-rms-client.md)组件可以在客户端或服务器操作系统上运行，包含使应用程序可以加密和解密内容、检索模板和吊销列表、从服务器获取许可证和证书以及执行其他相关权限管理任务的功能。

有关详细信息，请参阅[应用程序类型](application-types.md)。

以下只是几个可以应用在 Rights Management Services SDK 2.1 上构建的应用程序的方案。

-   一个律师事务所希望阻止打印或转发敏感电子邮件消息。
-   计算机辅助设计和制造软件的开发人员希望限制只有研发部门的一小组用户无需使用密码即可访问图纸。
-   图形设计网站的所有者希望使用单个许可证，该许可证允许免费查看其图像的较低分辨率副本，但需要付费才能访问高分辨率版本。
-   联机文档库的所有者希望基于用户身份启用查看、打印或编辑文档的权限。
-   公司希望将敏感员工信息发布到将查看和编辑权限限制到特定用户的内部网站。

有关 AD RMS 服务器、AD RMS 客户端及其功能的详细信息，请参阅 TechNet 内容以获取[针对 AD RMS 的 IT 专业人员文档](https://TechNet.Microsoft.Com/library/cc771234.aspx)。

本部分中的其余主题将介绍 RMS 体系结构及其实现。

## <a name="in-this-section"></a>本部分内容

| 主题 | 描述 |
|-------|-------------|
|[客户端](ad-rms-client.md) |本主题介绍 Rights Management Services 客户端 2.1 的用途和功能 |
|[服务器](ad-rms-server.md) | 本主题介绍适用于 Azure 和 Windows Server 的 RMS 服务器的用途和功能。|


## <a name="related-topics"></a>相关主题

* [RMS 概念](application-types.md)
* [入门](getting-started-with-ad-rms-2-0.md)
* [针对 AD RMS 的 IT 专业人员文档](https://technet.microsoft.com/library/cc771234.aspx)

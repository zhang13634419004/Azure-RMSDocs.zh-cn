---
title: 使用 FCI 的 Windows 文件服务器 Azure RMS-AIP 的支持方式
description: 部署 RMS 连接器时如何将 Windows Server 文件分类基础结构与 Azure RMS 结合使用以自动保护 Office 文档。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7e0a586490b54c9fcb798f3d1a8776262ff6847c
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136317"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>使用 FCI 的 Windows 文件服务器如何支持 Azure Rights Management

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


当你将 Windows Server 配置为使用文件分类基础结构时，此文件服务器资源管理器功能可以扫描本地文件，并确定它们是否包含敏感数据。 对于满足此条件的文件，可以使用管理员定义的分类属性，对其进行标记。 然后，文件分类基础结构可根据分类执行自动操作。 其中一项操作包括使用 Azure Rights Management 和 Rights Management 连接器（也称为 RMS 连接器）的部署来应用信息保护。 然后，由 Azure RMS 自动保护 Office 文件。

若要保护所有文件类型，请不要使用 RMS 连接器，而是改为运行 Windows PowerShell 脚本，该脚本使用 [Azure 信息保护模块](./rms-client/client-admin-guide-powershell.md)中的 cmdlet。

分类策略是完全可以配置的，并且具有高度的可扩展性，因此你可以防止未授权和已授权用户可能发生的数据泄漏。 它甚至有助于降低网络管理员的数据泄漏风险，因为你可以配置不要求这些管理员具有文件访问权限的策略。

有关为 Office 文件部署和配置 RMS 连接器的说明，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

有关对所有文件类型使用 Windows PowerShell 脚本的说明，请参阅[使用 Windows Server 文件分类基础结构的 RMS 保护 &#40;FCI&#41;](./rms-client/configure-fci.md)。



## <a name="next-steps"></a>后续步骤
至此，已了解应用程序和服务如何支持 Azure RMS，建议比较 Azure RMS 与本地版 Rights Management、Active Directory Rights Management Services (AD RMS)。 有关功能、要求和安全控制的比较，请参阅[比较 Azure Rights Management 和 AD RMS](compare-on-premise.md)。



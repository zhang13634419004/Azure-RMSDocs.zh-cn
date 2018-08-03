---
title: Azure 信息保护的要求
description: 确定为组织部署 Azure 信息保护的必备条件。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/27/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f126fe6b76a0d637e202d86bde9f257561c5a72e
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474684"
---
# <a name="requirements-for-azure-information-protection"></a>Azure 信息保护的要求

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

为组织部署 Azure 信息保护之前，请确保具备以下必备条件。 

## <a name="subscription-for-azure-information-protection"></a>Azure 信息保护订阅

**若要使用分类、设置标签和保护**，必须拥有 [Azure 信息保护计划](https://azure.microsoft.com/pricing/details/information-protection/)。 

**若仅需保护**，必须拥有[包括 Azure 信息保护的 Office 365计划](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。

若要确认组织的订阅包括所需的 Azure 信息保护功能，请查看 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)页面中的功能列表。

> [!TIP]
> 希望查看 Office 365 计划或 Exchange Online 独立计划是否支持 [Office 365 邮件加密的新增功能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)，以向个人电子邮件地址发送受保护的电子邮件？ 例如 Gmail、Yahoo 和 Microsoft。 请参阅以下资源：
>
> [Exchange Online 服务说明](https://technet.microsoft.com/library/exchange-online-service-description.aspx)
>
> [Office 365 教育版](https://technet.microsoft.com/library/mt844095.aspx)
>
> [Office 365 美国政府版](https://technet.microsoft.com/library/mt774581.aspx)

如果对订阅或许可有任何疑问，请勿将问题发布在此页面上，而是联系你的 Microsoft 客户经理或 [Microsoft 支持部门](information-support.md#to-contact-microsoft-support)。

## <a name="azure-active-directory"></a>Azure Active Directory

你的组织必须具有 Azure Active Directory (Azure AD) 才能支持用户身份验证和 Azure 信息保护身份授权。 此外，如果你希望使用本地目录 (AD DS) 中的用户帐户，则还必须配置目录集成。

Azure 信息保护支持单一登录 (SSO)，这样就不会反复提示用户输入凭据。 如果使用其他供应商解决方案进行联合，请与相应供应商确认如何针对 Azure AD 配置它。 WS-Trust 是这些解决方案支持单一登录所需满足的常见要求。 

具有所需客户端软件并正确配置 MFA 支持基础结构后，Azure 信息保护将支持多重身份验证 (MFA)。

预览版支持按条件访问受 Azure 信息保护进行保护的文档。 有关详细信息，请参阅以下常见问题解答：[我看到 Azure 信息保护被列为可用于条件访问的云应用 - 工作原理是什么？](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

有关身份验证要求的详细信息，请参阅 [Azure 信息保护的 Azure Active Directory 要求](requirements-azure-ad.md)。 

有关对用户和组帐户进行授权的要求的详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](./plan-design/prepare.md)。

## <a name="client-devices"></a>客户端设备

用户必须拥有运行支持 Azure 信息保护的操作系统的客户端设备（计算机或移动设备）。

以下设备支持 Azure 信息保护客户端，它可使用户分类并标记其文档和电子邮件：

- Windows 10（x86、x64）
    
    - 预览体验成员的 Windows 10 RS4 内部版本中不支持手写。 

- Windows 8.1（x86、x64）

- Windows 8（x86、x64）

- Windows 7 Service Pack 1（x86、x64）

- Windows Server 2016 

- Windows Server 2012 R2 和 Windows Server 2012

- Windows Server 2008 R2 

对于列出的服务器版本，远程桌面服务支持用于 Azure 信息保护客户端。 将 Azure 信息保护客户端与远程桌面服务结合使用时，如果删除用户配置文件，请勿删除“%Appdata%\Microsoft\Protect”文件夹。

当 Azure 信息保护客户端通过使用 Azure 权限管理服务保护数据时，支持 Azure 权限管理服务的[同一设备](requirements-client-devices.md)可以使用此数据。

Azure 信息保护客户端有[其他先决条件](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)，管理员指南中列出了这些条件。

## <a name="applications"></a>应用程序

Azure 信息保护客户端可使用以下 Office 版本中的 Word、Excel、PowerPoint 和 Outlook 等 Office 应用程序对文档和电子邮件设置标签和进行保护：

- 含 2016 应用或 2013 应用的 Office 365 ProPlus（即点即用或基于 Windows Installer 的安装）
    
    包含 Azure 信息保护数据保护的大多数 Office 365 订阅（并非所有）都附带这些版本的 Office。 检查你的订阅信息，确定是否包含 Office 365 专业增强版。 你还可以在 [Azure 信息保护数据表](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)中找到此信息。

- Office Professional Plus 2016

- Office Professional Plus 2013 Service Pack 1

- Office Professional Plus 2010 Service Pack 2

Office 的其他版本无法通过使用 Rights Management 服务保护文档和电子邮件。 对于这些版本，仅支持 Azure 信息保护分类。 因此，Azure 信息保护栏或 Office 功能区的“保护”按钮中不会向用户显示应用保护的标签。 

Azure 信息保护客户端不支持同一台计算机上的多个 Office 版本。 此客户端也不支持在 Office 中的不同用户帐户之间切换。

有关支持数据保护服务的 Office 版本的信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](requirements-applications.md)。

## <a name="firewalls-and-network-infrastructure"></a>防火墙和网络基础结构

如果你有配置为允许特定连接的防火墙或类似中介网络设备，请参阅以下 Office 文章的 [Office 365 门户和共享](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity)部分中有关 Azure 权限管理 (RMS) 的信息：[Office 365 URL 和 IP 地址范围](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。

使用此 Office 文章中的说明通过订阅 RSS 源来跟踪本信息的最新更改。

除了 Office 文章中特定于 Azure 信息保护的信息外：

- 允许 TCP 443 上的 HTTPS 流量流入 api.informationprotection.azure.com。

- 允许 TCP 443 上的 HTTPS 流量流入 mobile.pipe.aria.microsoft.com。

- 如果使用要求进行身份验证的 Web 代理，必须将其配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据配合使用。

- 不要终止 Azure Rights Management 服务的 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 这样做会中断 RMS 客户端用于 Microsoft 托管 CA 的证书固定，之所以使用固定是为了帮助保护它们与 Azure Rights Management 服务的通信安全。
    
    - 提示：鉴于 Chrome 在地址栏中显示安全连接的方式，可以使用此浏览器在访问 Azure Rights Management 服务前，快速检查客户端连接是否已终止。 请在此浏览器地址栏中输入以下 URL：`https://admin.na.aadrm.com/admin/admin.svc` 
    
        不必担心浏览器窗口显示什么内容。 相反，单击地址栏中的挂锁，即可查看网站信息。 在网站信息中，可以查看证书发证机构 (CA)。 如果证书不是由 Microsoft CA 颁发，表明客户端与服务的安全连接很可能即将终止，并需要重新配置防火墙。 下图中的示例展示了 Microsoft 证书发证机构 (CA)。 如果看到的是内部 CA 颁发的证书，表明此配置与 Azure 信息保护不兼容。
        
        ![检查为 Azure 信息保护连接颁发的证书](./media/certificate-checking.png)

### <a name="on-premises-servers"></a>本地服务器

如果想要将 Azure 信息保护中的 Azure Rights Management 服务与本地服务器配合使用，则支持以下产品：

- Exchange Server

- SharePoint Server

- 支持文件分类基础结构的 Windows Server 文件服务器

有关此方案的其他要求的信息，请参阅[支持 Azure Rights Management 数据保护的本地服务器](requirements-servers.md)。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS 和 Azure RMS 共存

不支持以下部署方案，除非将 AD RMS for [HYOK 保护](./deploy-use/configure-adrms-restrictions.md)与 Azure 信息保护配合使用（“自留密钥”配置）：

- 在同一个组织中并行运行 AD RMS 和 Azure RMS，除非是在迁移过程中，如[从 AD RMS 迁移到 Azure 信息保护](./plan-design/migrate-from-ad-rms-to-azure-rms.md)所述。

支持[从 AD RMS 到 Azure 信息保护](http://technet.microsoft.com/library/Dn858447.aspx)和[从 Azure 信息保护到 AD RMS](/powershell/module/aadrm/Set-AadrmMigrationUrl) 的迁移路径。 如果你部署 Azure 信息保护，然后决定不再想要使用此云服务，请参阅[解除 Azure 信息保护授权和停用 Azure 信息保护](./deploy-use/decommission-deactivate.md)。




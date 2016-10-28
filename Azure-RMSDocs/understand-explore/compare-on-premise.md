---
title: "比较 Azure 信息保护与 AD RMS |Azure 信息保护"
description: "如果你了解或以前部署过 Active Directory Rights Management Services (AD RMS)，你可能想知道 Azure 信息保护在功能和要求方面与它相比有何差别。"
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4591d5c45104108ccf151bb1d7a9382652e585a6
ms.openlocfilehash: 36adf768bdb5a0937af3563665bbe139c86ff250


---

# 比较 Azure 信息保护与 AD RMS

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*

如果你了解或以前部署过 Active Directory Rights Management Services (AD RMS)，你可能想知道 Azure 信息保护作为信息保护解决方案在功能和要求方面与它相比有何差别。

Azure 信息保护的一些主要差异：

- **不需要服务器基础结构**：Azure 信息保护不需要 AD RMS 所需的额外服务器和 PKI 证书，因为 Microsoft Azure 将处理这些内容。 因而这一云解决方案可以更快部署且更易维护。

- **基于云的身份验证**：对于内部用户和来自其他组织的用户，Azure 信息保护都使用 Azure AD 进行身份验证。 这意味着即使移动用户未连接到你的内部网络，也可对其进行身份验证，并且你可以更轻松地与来自其他组织的用户共享受保护的内容。 许多组织由于运行 Azure 服务或使用 Office 365，因而在 Azure AD 中已拥有用户帐户。 但如果没有，用户可通过个人 RMS 创建免费帐户。 若要与其他组织共享受 AD RMS 保护的内容，则需要对每个组织配置显式信任。

- **对移动设备的内置支持**：无需进行部署更改，Azure RMS 即可支持移动设备和 Mac 计算机。 若要使 AD RMS 支持这些设备，必须安装移动设备扩展、配置 AD FS 以便进行联合身份验证，并为公共 DNS 服务创建其他记录。

- **默认模板**：激活 Azure 信息保护后，该保护服务将创建两个默认模板，让你可以非常轻松地立即开始保护重要数据。 AD RMS 无默认模板。

- **部门模板**：Azure 信息保护支持部门模板，它是你所创建额外模板的一项配置设置。 此设置允许指定可以在其客户端应用程序（例如 Office 应用）中看到该模板的用户，让他们能够更轻松地选择你为不同用户组选择定义的适当策略。 AD RMS 不支持部门模板。

- **文档跟踪、吊销和电子邮件通知**：Azure 信息保护通过 RMS 共享应用支持这些功能，而 AD RMS 不支持。

- **分类和标签**： Azure 信息保护通过与 Office 应用程序集成的 Azure 信息保护栏支持这些功能，而 AD RMS 不支持。


此外，由于 Azure 信息保护是一项云服务，因此与基于本地服务器的解决方案相比，它可以更快交付新功能和修补程序。 Windows Server 2016 中未为 AD RMS 规划新功能。

有关详细信息和其他差别，请使用以下表格并排比较 Azure 信息保护和 AD RMS 的功能和优势。 如果你有安全方面的比较问题，请参阅本文中的[签名和加密的加密控制](compare-azure-rms-ad-rms.md#cryptographic-controls-for-signing-and-encryption)。

> [!NOTE]
> 为了简化这种比较，本文重复了 [Azure 信息保护的要求](../get-started/requirements-azure-rms.md)中的一些信息。 使用该资源了解有关 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的更具体的支持和版本信息。

|Azure 信息保护|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|支持 Microsoft Online Services（例如  Exchange Online 和 SharePoint Online 以及 Office 365）中的信息权限管理 (IRM) 功能。<br /><br />还支持本地 Microsoft 服务器产品，例如 Exchange Server、SharePoint Server 以及运行 Windows Server 和文件分类基础结构 (FCI) 的文件服务器。|支持本地 Microsoft 服务器产品，例如 Exchange Server、SharePoint Server 以及运行 Windows Server 和文件分类基础结构 (FCI) 的文件服务器。|
|实现组织之间和任何组织内用户之间的隐式信任。 这意味着在用户使用 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 或 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]的情况下，或在用户注册了个人 RMS 的情况下，受保护内容可在同一组织或不同组织的用户之间共享。|信任必须在两个组织间以直接点对点的关系显式定义，方法是使用受信任用户域 (TUD) 或使用 Active Directory 联合身份验证服务 (AD FS) 创建的联合信任。|
|提供两个默认权限策略模板，将内容的访问权限仅限于自己的组织范围内；一个模板提供受保护内容的只读查看，另一个模板提供受保护内容的写入或修改权限。<br /><br />你还可以创建自己的自定义模板，其中包括只对用户的子集可见的部门模板。 有关详细信息，请参阅[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)。<br /><br />此外，如果模板不能满足需求，用户可以定义自己的一组权限。|没有默认权限策略模板；必须创建这些模板，然后分发它们。 有关详细信息，请参阅 [AD RMS 策略模板注意事项](http://go.microsoft.com/fwlink/?LinkId=154765)。<br /><br />此外，如果模板不能满足需求，用户可以定义自己的一组权限。|
|支持的 Microsoft Office 最低版本为 Office 2010，它需要 [RMS 共享应用程序](../rms-client/sharing-app-windows.md)。<br /><br />Microsoft Office for Mac：<br /><br />- Microsoft Office for Mac 2016：受支持<br /><br />- Microsoft Office for Mac 2011：不受支持|支持的 Microsoft Office 最低版本为 Office 2007。<br /><br />Microsoft Office for Mac：<br /><br />- Microsoft Office for Mac 2016：受支持<br /><br />- Microsoft Office for Mac 2011：受支持|
|支持适用于 Windows、Mac 计算机和移动设备的 [RMS 共享应用程序](../rms-client/sharing-app-windows.md)。<br /><br />此外，RMS 共享应用程序支持以下内容：<br /><br />- 与其他组织的用户共享。<br /><br />- 电子邮件通知，让发件人知道有人尝试打开受保护附件。<br /><br />- 适用于用户的文档跟踪站点，包括撤消文档的功能。|支持适用于 Windows、Mac 计算机和移动设备的 [RMS 共享应用程序](../rms-client/sharing-app-windows.md)。 但是，共享不支持与其他组织的用户共享、电子邮件通知、或文档跟踪站点以及用户撤消文档的功能。|
|可以在使用 RMS 共享应用程序时，通过[本机保护或常规保护](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)，保护所有文件类型。<br /><br />对于其他应用程序，检查[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)中的表。|可以在使用 RMS 共享应用程序时，通过[本机保护或常规保护](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)，保护所有文件类型。<br /><br />对于其他应用程序，检查[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)中的表。|
|支持的 Windows 客户端最低版本为 Windows 7。|支持的 Windows 客户端最低版本为 Windows Vista Service Pack 2。|
|移动设备支持包括 Windows Phone、Android、iOS 和 Windows RT。<br /><br />在支持 Exchange ActiveSync IRM 协议的所有移动设备平台上，也支持使用该协议管理电子邮件。|移动设备支持包括 Windows Phone、Android、iOS 和 Windows RT，并需要 [Active Directory Rights Management 服务移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx)。<br /><br />在支持 Exchange ActiveSync IRM 协议的所有移动设备平台上，支持使用 Exchange ActiveSync IRM 管理电子邮件。|
|支持适用于计算机和移动设备的多因素身份验证 (MFA)。<br /><br />有关详细信息，请参阅[多重身份验证 (MFA) 和 Azure 信息保护](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms)。|如果将 IIS 配置为请求证书，将支持智能卡身份验证。|
|支持加密模式 2，而无需额外配置，该模式针对各种密钥长度和加密算法提供更强大的安全性。<br /><br />有关详细信息，请参阅本文中的[对签名和加密的加密控制](#cryptographic-controls-for-signing-and-encryption)部分以及 [AD RMS 加密模式](http://go.microsoft.com/fwlink/?LinkId=266659)。|默认情况下支持加密模式 1，需要额外配置才能支持加密算法 2，以提供更强大的安全性。<br /><br />有关详细信息，请参阅本文中的[对签名和加密的加密控制](#cryptographic-controls-for-signing-and-encryption)部分以及 [AD RMS 加密模式](http://go.microsoft.com/fwlink/?LinkId=266659)。|
|支持从 AD RMS 迁移，如果需要，支持迁移到 AD RMS：<br /><br />- [从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [解除 Azure 信息保护授权和停用 Azure 信息保护](../deploy-use/decommission-deactivate.md)|支持从 Azure 信息保护迁移以及迁移到 Azure 信息保护：<br /><br />- [解除 Azure Rights Management 授权和停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)<br /><br />- [从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|需要 Azure 信息保护许可证才能保护内容。 无需 Azure 信息保护许可证即可使用已受 Azure 信息保护（包括另一个组织的用户）保护的内容。<br /><br />有关详细信息，请参阅 Azure 信息保护网站上的[功能列表](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)。|需要 RMS 许可证才能保护内容，以及使用已受 AD RMS 保护的内容。<br /><br />有关 AD RMS 授权的详细信息，如果是一般信息，请参阅 [客户端访问许可证和管理许可证](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) ，如果是特定信息，请联系 Microsoft 合作伙伴或 Microsoft 代表。|

## 对签名和加密的加密控制
Azure 信息保护始终将 RSA 2048 用于所有公钥加密，将 SHA 256 用于签名操作。 相比之下，AD RMS 支持 RSA 1024 和 RSA 2048，还将 SHA 1 或 SHA 256 用于签名操作。

Azure 信息保护和 AD RMS 都将 AES 128 用于对称加密。

如果创建了租户密钥并由 Microsoft 管理（默认），或者如果你管理自己的租户密钥（称为 BYOK），Azure 信息保护将遵守 FIPS 140-2。 有关管理租户密钥的详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)。

## 后续步骤
如果希望从 AD RMS 迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)





<!--HONumber=Oct16_HO1-->


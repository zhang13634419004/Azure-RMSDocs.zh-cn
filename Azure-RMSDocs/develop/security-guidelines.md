---
title: "安全最佳实践 | Microsoft 信息保护"
description: "启用 RMS 的应用程序是使用 Azure 信息保护最佳实践构建的。"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 12/06/2016
ms.topic: article
ms.prod: 
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.technology: techgroup-identity
ms.suite: ems
ms.reviewer: kartikk
translationtype: Human Translation
ms.sourcegitcommit: 2142a13d742b2dc0b59c3b996db69406cd818149
ms.openlocfilehash: b225a923b7f067fd7dc0ca67742275e399a8aa7c

---

# <a name="security-best-practices-for-azure-information-protection"></a>Azure 信息保护的安全最佳实践

Azure 信息保护 (AIP) 软件开发工具包 (SDK) 提供可靠的系统，用于发布和使用所有类型的受保护信息。 为了帮助 AIP 系统尽可能的强大，启用 AIP 的应用程序必须使用 AIP 最佳实践进行构建。 启用 AIP 的应用程序共同分担责任，帮助维持此生态系统的安全。 识别安全风险，并为应用程序开发期间引入的风险提供缓解，在最大程度上减小不安全的软件实现的可能性。

使用 Azure 信息保护软件开发工具包 (SDK) 实现应用程序的最佳实践包括以下类别的建议：
- [Threat Models and Mitigations](https://msdn.microsoft.com/en-us/library/aa362751.aspx)（威胁模型和缓解）
- [Security Attacks](https://msdn.microsoft.com/en-us/library/aa362736.aspx)（安全攻击）

此信息补充了必须签署的法律协议，以获取使用 AIP SDK 实现应用程序所需的数字证书。

## <a name="subjects-not-covered-in-these-topics"></a>这些主题中不包括使用者的相关内容
这些主题简要说明了以下问题，这些问题在尝试创建开发环境和安全应用程序时至关重要：
- **软件开发过程管理** - 包括配置管理、保护源代码、在最大程度上减少对已调试代码的访问以及为 Bug 分配优先级的相关信息。 对一些客户而言，拥有更安全的软件开发过程至关重要。 有些客户甚至会规定开发过程。
- **常见编码错误** - 包括避免缓冲区溢出的相关信息。 建议使用 Michael Howard 和 David LeBlanc 最新版本的编写安全代码 (Microsoft Press, 2002) 查看这些一般威胁和缓解。
- **社会工程** - 包含过程化和结构化安全措施的相关信息，这些措施有助于防止开发人员或制造商组织内部的其他人员私自利用代码。
- **物理安全性** - 包括锁定对代码基和签名证书的访问权限的相关信息。
- **预发行软件的部署或分发** - 包括分发 Beta 版本软件的相关信息。
- **网络管理** - 包括物理网络上入侵检测系统的相关信息。

## <a name="threat-models-and-mitigations"></a>威胁模型和缓解
数字信息所有者需要能够评估其资产在其中解密的环境。 最低安全标准的声明可以为信息所有者提供一个框架，用于理解和评估他们向其委托信息的应用程序的安全级别。

某些行业（如政府和卫生保健行业）拥有可能适用于产品的证书以及认证过程和标准。 满足这些最低安全建议并不能替代客户独特的认证需求。 然而，安全标准的目的在于帮助你做好应对客户目前和未来需求的准备，并且有助于使在开发周期初期进行的任何投资有益于应用程序。 这些都只是建议，并不是正式的 Microsoft 认证计划。

权限管理服务系统中存在以下几个主要的漏洞类别，包括：
- **泄露** - 信息出现在未经授权的位置。
- **损坏** - 软件或数据以未经授权的方式被修改。
- **拒绝** - 计算资源不可用。

这些主题重点关注“泄漏”问题。 API 系统的完整性依赖于随着时间的推移其保护信息的能力，即仅允许访问指定的实体。 这些主题也会涉及“损坏”问题。 不包括任何“拒绝”问题。

Microsoft 不会测试或审查与满足最低标准相关的测试结果；完全由合作伙伴来确保满足最低标准。 Microsoft 提供两个附加级别的建议，以帮助缓解常见威胁。 一般情况下，这些建议都是添加的；例如，除非另外指定，否则如果符合首选建议，则假设已满足了最低标准（如适用）。

|标准级别|    描述|
|---|---|
|最低标准|  必须先确定处理 AIP 受保护信息的应用程序满足最低标准，才能使用从 Microsoft 收到的生产证书对该应用程序进行签名。 通常情况下，合作伙伴只有在自己的内部测试已验证应用程序满足此最低标准后最终发行软件时，才会使用生产层次结构证书。 满足最低标准并不是，并且也不应被认为是 Microsoft 提供的安全保证。 Microsoft 不测试或审查与满足最低标准相关的测试结果；完全由合作伙伴确保满足最低标准。|
|建议的标准|  建议的准则既描绘了改进应用程序安全性的途径，又指出了在实现更多安全条件的同时 AIP 可能会如何发展。 供应商可能会尝试通过构建此更高级别的安全准则来区分其应用程序。|
|首选标准|    这是当前定义的最高安全类别。 开发被标记为高度安全的应用程序的供应商应以此标准为目标。 遵循此标准的应用程序可能最不容易受到攻击。|




## <a name="malicious-software"></a>恶意软件
Microsoft 已定义了应用程序必须满足的最低要求标准，以保护内容免受恶意软件的攻击。

### <a name="importing-malicious-software-by-using-address-tables"></a>使用地址表导入恶意软件
AIP 不支持在运行时修改代码或修改导入地址表 (IAT)。 会为加载在进程空间中的每个 DLL 创建一个导入地址表。 它指定应用程序导入的所有函数的地址。 一个常见的攻击是修改应用程序中的 IAT 条目，例如将其修改为指向恶意软件。 AIP 在检测到此类攻击时会停止应用程序。

### <a name="minimum-standard"></a>最低标准
- 无法在执行期间修改应用程序进程中的导入地址表。 - 应用程序指定许多在运行时通过使用地址表调用的函数，无法在运行时期间或之后更改这些函数。 除此之外，这意味着无法对通过使用生产证书签名的应用程序执行代码分析。
- 无法从清单中指定的任何 DLL 内调用 **DebugBreak ** 函数。
- 无法调用具有 **DONT_RESOLVE_DLL_REFERENCES** 标志设置的 **LoadLibrary**。 此标志会指示加载器跳过绑定到导入的模块，因此修改了导入地址表。
- 无法通过对 /DELAYLOAD 链接器开关执行运行时或后续更改来更改延迟加载。
- 无法通过提供自己拥有的 Delayimp.lib helper 函数版本来更改延迟加载。
- 存在 AIP 环境时，无法卸载由已通过验证的模块延迟加载的模块。
- 无法使用 **/DELAY:UNLOAD** 链接器开关启用延迟模块卸载。


## <a name="incorrectly-interpreting-license-rights"></a>错误地解释许可证权限

如果应用程序没有正确地解释并强制执行 AIP 发行许可证中所表达的权限，则可能会以信息所有者不希望的方式提供信息。 该情况的一个示例是在发行许可证仅授予查看信息权限的情况下，应用程序允许用户将未加密的信息保存到新的介质。

AIP 系统将权限编为几组。 有关详细信息，请参阅 [Configuring usage rights for Azure Rights Management](../deploy-use/configure-usage-rights.md)（为 Azure Rights Management 配置使用权限）。

### <a name="azure-information-protection"></a>Azure 信息保护  
API 允许用户解密或不解密信息；该信息没有任何固有保护。 如果用户有权解密信息，API 则允许此操作，并且在解密完成后，应用程序会负责管理或保护该信息。 应用程序负责管理其环境和接口，以防止未经授权使用信息的行为；例如，如果许可证仅授予“播放”权限，则会禁用“打印”和“复制”按钮。 测试套件应验证应用程序是否根据其所识别的所有许可证权限进行正确地操作。

### <a name="minimum-standard"></a>最低标准
- 如 XrML 规范中所述，XrML v.1.2 权限的客户实现应与这些权限的定义相一致，可在 XrML 网站 (http://www.xrml.org) 上查看这些规范。 必须为所有对应用程序感兴趣的实体定义特定于应用程序的权限。
- 测试套件和测试过程应验证应用程序是否根据应用程序所支持的权限进行正确地操作，并且没有根据不受支持的权限进行操作。
- 如果要构建发布应用程序，则必须提供可用的信息，这些信息说明发布应用程序支持和不支持的内部权限，以及如何解释这些权限。 此外，用户界面应向最终用户说明每个权限授予或拒绝个别信息的含义。

- 需要将由应用程序实现的新权限中包含的内容所抽象化的任何权限映射到新的术语。 例如，名为 MANAGER 的新权限可能将 PRINT、COPY 和 EDIT 权限包括为抽象权限。
建议标准（暂时没有）。
首选标准（暂时没有）。



<!--HONumber=Dec16_HO2-->


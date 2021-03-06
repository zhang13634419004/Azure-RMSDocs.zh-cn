---
title: 分类和标签的常见问题解答 - AIP
description: 使用 Azure 信息保护进行分类和设置标签时遇到问题？ 请查看此处是否有答案。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 20698241962b8dfe3e1fd81b7f0538a7ddfdd46a
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802175"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>有关 Azure 信息保护中的分类和标签的常见问题

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）  和标签管理  将于 2021 年 3 月 31 日  弃用  。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

遇到有关 Azure 信息保护的专门与分类和标签有关的问题？  请查看此处是否有答案。 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>我应该安装哪个客户端来测试新功能？

目前有两个适用于 Windows 的 Azure 信息保护客户端： 

- **Azure 信息保护统一标签客户端**，它从以下管理中心之一下载标签和策略设置： Office 365 Security & 相容性中心、Microsoft 365 安全中心、Microsoft 365 合规中心。 此客户端现已正式发布，并且可能有一个预览版本，你可以在将来的版本中测试其他功能。

- **Azure 信息保护客户端 (经典) **从 Azure 门户下载标签和策略设置。 此客户端建立在以前的客户端通用版本上。

如果客户的当前功能集和功能满足你的业务要求，我们建议你与统一的标签客户端进行测试。 否则，或者如果已在尚未[迁移到统一标签存储](configure-policy-migrate-labels.md)的 Azure 门户中配置了标签，请使用经典客户端。

有关详细信息，包括特性和功能的比较表，请参阅[选择使用哪个 Azure 信息保护客户端](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)。

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>在哪里可以找到有关使用 Office 应用的敏感度标签的信息？

请参阅以下文档资源：

- [了解敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) 

- [Office 应用中的敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)

- [向 Office 中的文档和电子邮件应用敏感度标签](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

## <a name="can-a-file-have-more-than-one-classification"></a>文件是否可以有多个分类？

用户一次仅可为每个文档或电子邮件选择一个标签，这通常只会产生一个分类。 但如果用户选择子标签，这实际上会同时应用两个标签；主标签和次要标签。 通过使用子标签，文件可以有两个分类，表示附加控制级别的父\子关系。

例如，标签“机密”**** 可能包含子标签，如“法律”**** 和“财务”****。 可对这些子标签应用不同的分类视觉标记和不同的权限管理模板。 用户不能自行选择“机密”**** 标签；只能选择其中一个子标签，如“法律”****。 因此，会看到设置的标签是“机密\法律”****。 该文件的元数据包括“Confidential”**** 的一个自定义文本属性和“Legal”**** 的一个自定义文本属性，以及另一个同时包含这两个值（“Confidential Legal”****）的自定义文本属性。 

使用子标签时，请不要在主标签处配置视觉标记、保护和条件。 使用子级别时，请仅在子标签上配置这些设置。 如果在主标签及其子标签上配置这些设置，那么子标签上的设置具有更高优先级。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>如何防止他人删除或更改标签？

尽管有一个[策略设置](configure-policy-settings.md)要求用户指出为什么要降低分类标签、删除标签或删除保护的原因，但此设置不会阻止这些操作。 要防止用户删除或更改标签，内容必须已受到保护，并且保护权限不向用户授予导出或完全控制[使用权限](configure-usage-rights.md)。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>标记一封电子邮件时，是否有任何附件会自动获得相同的标记？

错误。 标记有附件的电子邮件时，这些附件不会继承相同的标记。 附件仍不带标签，或者保留单独应用的标签。 不过，如果电子邮件的标签应用了保护配置，此保护配置也会应用于 Office 附件。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP 解决方案和其他应用如何与 Azure 信息保护相集成？

因为 Azure 信息保护将永久性元数据用于分类（包括明文标签），所以此信息可供 DLP 解决方案和其他应用程序读取。 

有关此元数据的详细信息，请参阅[电子邮件和文档中存储的标签信息](configure-policy.md#label-information-stored-in-emails-and-documents)。

有关将此元数据与 Exchange Online 邮件流规则配合使用的示例，请参阅[配置 Azure 信息保护标签的 Exchange Online 邮件流规则](configure-exo-rules.md)。

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>我能否创建自动包含分类的文档模板？

是的。 可以将标签配置为，[应用包含标签名称的页眉或页脚](configure-policy-markings.md)。 但如果不满足你的要求，则仅 (经典) 的 Azure 信息保护客户端，你可以创建具有所需格式的文档模板，并将分类添加为字段代码。 

例如，文档的页眉中可能有一个显示分类的表。 或者，对引用文档分类的简介使用具体的字词。

若要在文档中添加此域代码，请执行以下操作：

1. 标记并保存文档。 此操作新建可立即用于域代码的元数据字段。

2. 在文档中，将光标置于要添加标签分类的位置，再在“插入”**** 选项卡中依次选择“文本”**** > “文档部件”**** > “字段”****。

3. 在“字段”**** 对话框中，选择“类别”**** 下拉列表中的“文档信息”****。 然后，选择“字段名称”**** 下拉列表中的“DocProperty”****。

4. 在“属性”**** 下拉列表中，依次选择“敏感度”**** 和“确定”****。

此时，当前标签的分类显示在文档中，并且这个值会在你每次打开文档或使用模板时自动刷新。 因此，如果标签发生更改，那么对此域代码显示的分类也会在文档中自动更新。

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>使用 Azure 信息保护的电子邮件分类与 Exchange 邮件分类有何不同？

交换消息分类是一项较旧的功能，可对电子邮件进行分类，并且独立于 Azure 信息保护标签或应用分类的敏感度标签。

但是，你可以将此较旧的功能与标签集成，以便当用户使用 Outlook web 上的 Outlook 以及使用某些移动邮件应用程序对电子邮件进行分类时，会自动添加标签分类和相应的标签标记。

可以使用同一技术将标签用于 Outlook 网页版和这些移动邮件应用程序。

请注意，如果在使用 Exchange Online 的 web 上使用 Outlook，则无需执行此操作，因为这种组合在从 Office 365 Security & 相容性中心、Microsoft 365 安全中心或 Microsoft 合规中心发布敏感度标签时支持内置标签。

如果无法在 web 上使用 Outlook 内置标签，请参阅此解决方法的配置步骤：[与旧 Exchange 消息分类的集成](rms-client/client-admin-guide-customizations.md#integration-with-the-legacy-exchange-message-classification)
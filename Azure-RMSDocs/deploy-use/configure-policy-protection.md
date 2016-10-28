---
title: "如何配置标签以应用 Rights Management 保护 | Azure 信息保护"
description: "你可以使用权限管理服务的加密、标识和授权策略保护最敏感的文档和电子邮件，以帮助防止数据丢失。 配置标签以使用权限管理模板时，将应用此保护。"
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 830e982fc1f0443545942c1deb1a2fc93431be17


---

# 如何配置标签以应用权限管理保护

>*适用于：Azure 信息保护*

你可以使用权限管理服务的加密、标识和授权策略保护最敏感的文档和电子邮件，以帮助防止数据丢失。 配置标签以使用权限管理模板时，将应用此保护。 

此模板可以是激活 Azure 权限管理时自动创建的默认模板或自定义模板之一。 支持 Azure 权限管理部门模板，但仅当文档或电子邮件作者属于模板配置的作用域时应用保护。 如果用户不在作用域内，则会看到 Azure 信息保护不能应用标签的消息。

## 保护的工作原理

当文档或电子邮件受权限管理保护时，它会在处于静态时和传输过程中进行加密，并且只能由授权用户进行解密。 文档或电子邮件的这种加密保持不变，即使将其重命名。 此外，你可以配置使用权限和限制，如下面的示例：

- 只有组织内的用户才能打开公司机密文档或电子邮件。

- 只有市场营销部门的用户才能编辑和打印促销通知文档或电子邮件，而组织中的所有其他用户只能阅读该文档或电子邮件。

- 用户不能转发包含内部重组相关新闻的电子邮件。

- 不能在指定日期后打开发送给业务合作伙伴的当前价目表。

有关 Azure 权限管理模板以及如何配置这些使用权限和限制的详细信息，请参阅[为 Azure 权限管理服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

有关 Azure 权限管理及其工作原理的详细信息，请参阅 [什么是 Azure 权限管理？](../understand-explore/what-is-azure-rms.md)(#什么是-azure-权限管理？)

> [!IMPORTANT]
> 若要配置标签以应用 Azure 权限管理保护，必须为组织激活 Azure 权限管理服务。 如果尚未这样做，请参阅 [激活 Azure 权限管理](../deploy-use/activate-service.md)(#激活-azure-权限管理)。


## 配置标签以应用权限管理保护

1. 如果尚未这样做，请打开一个新的浏览器窗口并以全局管理员的身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 

    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在“**Azure 信息保护**”边栏选项卡上，选择要配置为可视标记的标签以应用权限管理保护。

3. 在“标签”边栏选项卡的“设置 RMS 模板以保护包含此标签的文档和电子邮件”部分的“RMS 模板选择自”中，选择“Azure RMS”或“AD RMS (预览版)”。
    
    在大多数情况下，你将选择“Azure RMS”。 请勿选择 AD RMS（有时称为“*自留密钥*”(HYOK)），除非你已阅读并理解此配置附带的先决条件和限制。 有关详细信息，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。
    
4. 如果选择了 Azure RMS：对于“选择 RMS 模板”，请单击下拉框，并选择想要用来保护带有此标记的文档和电子邮件的[模板](../deploy-use/configure-custom-templates.md)或 Rights Management 选项。
    
    有关选项的详细信息：
    
    - 是否已在打开“标签”边栏选项卡后创建了新的模板？ 关闭此边栏选项卡，并返回到步骤 2，以便从 Azure 中检索新创建的模板供你选择。
    
    - 如果选择**部门模板**，或者如果已配置[载入控件](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)：
    
        - 配置的模板作用域外的用户或从应用 Azure 权限管理保护中排除的用户仍将看到该标签，但不能应用该标签。 如果他们选择该标签，则会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**
        
    - 如果选择“移除保护”:
        
        - 用户必须具有删除 Rights Management 保护的权限，以应用具有此选项的标签。 此选项要求它们具有**导出**（针对 Office 文档）或**完全控制**[使用权限](../deploy-use/configure-usage-rights.md)，或者为 Rights Management 所有者（自动授予完全控制使用权限）或者为 [Azure Rights Management 的超级用户](../deploy-use/configure-super-users.md)。 默认 Rights Management 模板不包括允许用户删除保护的使用权限。 

            如果用户不具有删除 Rights Management 保护的权限，并选择此具有“移除保护”选项的标记，他们将会看到以下消息：**Azure 信息保护无法应用此标记。如果此问题仍然存在，请与管理员联系。**

5. 如果选择了 AD RMS：请提供 AD RMS 群集的模板 GUID 和授权 URL。 [更多信息](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

6. 单击“保存” 。

7. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  



<!--HONumber=Oct16_HO1-->


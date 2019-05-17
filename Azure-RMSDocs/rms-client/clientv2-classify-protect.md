---
title: 分类和保护-Azure 信息保护统一标记的客户端
description: 有关如何进行分类和保护文档和电子邮件时使用 Azure 信息保护统一标记适用于 Windows 的客户端的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 1b05cf8f5194c8491a2aa7bb687622e821e770cb
ms.sourcegitcommit: 2fe9333c3e6c98e7dd9003c5f4cd7c1e7a48b297
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2019
ms.locfileid: "64880115"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-unified-labeling-client"></a>用户指南：分类和保护 Azure 信息保护统一标记客户端

>适用对象：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）*
>
> 说明：*[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> 借助这些说明，对文档和电子邮件进行分类和保护。 如果只需对文档和电子邮件进行分类（但不保护），请参阅[仅分类说明](clientv2-classify.md)。 如果不确定应使用哪组说明，请与管理员或支持人员核实。

在 Office 桌面应用中创建和编辑文档和电子邮件时对其进行分类和保护最为简单：Word、Excel、PowerPoint、Outlook。 

但是，还可以使用文件资源管理器对文件进行分类和保护。 此方法支持其他文件类型，此方法是一种一次性对多个文件进行分类和保护的便捷方法。 此方法支持保护 Office 文档、PDF 文件、文本和图像文件，以及各种其他文件。 

如果标签将保护应用于文档，则受保护的文档不适合保存在 SharePoint 或 OneDrive 中。 这些位置不支持受保护文件的以下内容：共同创作、Office Online、搜索、文档预览、缩略图和电子数据展示。

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>与组织外部人员安全共享文件

受保护文件可安全地与他人共享。 例如，你将受保护的文档附加到一封电子邮件。

在与组织外部人员共享文件之前，请咨询你的支持人员或管理员如何为外部用户保护文件。

例如，如果你的组织定期与另一组织中的人员进行通信，则管理员可能已经配置了设置保护以便这些人员可以阅读和使用受保护文档的标签。 然后，选择这些标签对要共享的文档进行分类和保护。

或者，如果有外部用户[企业到企业 (B2B) 帐户](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)为其创建，你可以使用[文件资源管理器来设置自定义权限](#using-file-explorer-to-classify-and-protect-files)文档在共享前。 如果设置你自己的自定义权限，并且文档已受到保护以供内部使用，请先创建一个副本来保留原始权限。 然后，使用此副本设置自定义权限。


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类和保护

从**主页**选项卡上，选择**敏感度**功能区中，按钮，然后选择一个已为你配置的标签。 例如：

![敏感度按钮示例](../media/sensitivity-not-set-callout.png)

或者，如果所选**显示数据条**从**敏感度**按钮，您可以从 Azure 信息保护栏选择标签。 例如：

![Azure 信息保护栏示例](../media/info-protect-barv2-not-set-callout.png)

若要设置一个标签，如"**Confidential** \ **所有员工**"，选择**机密**，然后**所有员工**。 如果你不确定要将哪种标签应用于当前文档或电子邮件，请使用标签工具提示详细了解每种标签及其应用情况。 如果已将某种标签应用于文档，并且想要进行更改，可以选择其他标签。 如果已经显示了 Azure 信息保护栏中，并且不为您进行选择，首先单击栏上显示标签，则**编辑标签**图标，当前标签值旁边。

除了手动选择标签，还可通过以下方式应用标签：

- 管理员配置了默认标签，你可保留或更改该标签。

- 您的管理员配置标签以检测到敏感信息时自动设置。

- 管理员配置时，建议使用标签检测到敏感信息时，系统会提示你接受此建议 （和应用标签），或拒绝它 （不应用建议的标签）。

### <a name="exceptions-for-the-sensitivity-button"></a>敏感度按钮的异常

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>看不到 Office 应用程序中的敏感度按钮？

- 您可能不具有 Azure 信息保护统一标记客户端[安装](install-unifiedlabelingclient-app.md)。

- 如果没有看到**敏感度**按钮在功能区上，但看**保护**按钮与标签，则必须安装了 Azure 信息保护客户端并不在 Azure 信息保护统一标记的客户端。 [详细信息](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>没有显示希望看到的标签？ 

可能的原因：

- 如果管理员最近为你配置了新标签，请尝试关闭 Office 应用程序的所有实例，然后重新打开。 此操作将检查对你的标签所做的更改。

- 如果缺少应用保护的标签，那么可能你使用的 Office 版本不支持应用 Rights Management 保护。 若要验证，单击“保护” > “帮助和反馈”。 在对话框中，检查“客户端状态”部分中是否显示消息“此客户端未获许可使用 Office Professional Plus”。 
    
    如果你有 Office 365 商业版或 Microsoft 365 商业版中的 Office 应用，则无需使用 Office 专业增强版，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证。

- 此标签采用的作用域策略可能不包括你的帐户。 请与你的技术支持或管理员一起检查。


### <a name="safely-sharing-by-email"></a>通过电子邮件实现安全共享

通过电子邮件共享 Office 文档时，可将文档附加到所保护的电子邮件中，应用到此电子邮件的相同限制会自动保护此文档。 

但是，你可能想要首先，保护文档，然后将其附加到电子邮件。 如果电子邮件中包含敏感信息，也需要保护电子邮件。 保护文档，然后将其附加到电子邮件的好处：

- 可以对文档应用不同于电子邮件的权限。

## <a name="using-file-explorer-to-classify-and-protect-files"></a>使用文件资源管理器对文件进行分类和保护

使用文件资源管理器时，可快速对单个文件、多个文件或文件夹进行分类和保护。 

选择文件夹时，将自动为你设置的分类和保护选项选择该文件夹及其所有子文件夹中的所有文件。 但是，在该文件夹或子文件夹中创建的新文件不会自动配置这些选项。

使用文件资源管理器对文件进行分类和保护时，如果一个或多个标签显示为灰色，则你选择的文件不支持分类。 对于这些文件，只有在管理员已将标签配置为应用保护时，你才能选择标签。 或者，你可以指定自己的保护设置。 

分类和保护会自动排除一些文件，因为更改这些文件可能会导致电脑停止运行。 尽管你可以选择这些文件，但系统会将其作为排除的文件夹或文件跳过。 示例包括可执行文件和你的 Windows 文件夹。

管理员指南包含受支持文件类型的完整列表以及自动排除的文件和文件夹的完整列表：[支持 Azure 信息保护统一标记客户端的文件类型](clientv2-admin-guide-file-types.md)。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>使用文件资源管理器对文件进行分类和保护

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。 例如：
    
    ![在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”](../media/right-click-classify-protect-folder.png)

2. 在“分类和保护 - Azure信息保护”对话框中，请像在 Office 应用程序中那样使用标签，这样可以按管理员定义的方式设置分类和保护。 

   - 如果没有标签可以选择（它们呈灰显状态）：所选文件不支持分类，但可以通过自定义权限保护它（步骤 3）。 例如：

     ![“分类和保护 - Azure 信息保护”对话框中无可用标签](../media/v2info-protect-dialog-labels-dimmed.png)

3. 可以指定您自己的保护设置，而不是在所选标签使用管理员可能已包含的保护设置。 若要执行此操作，请选择“使用自定义权限进行保护”。
    
    指定的任何自定义权限将替换而不是补充管理员可能已为所选标签定义的保护设置。  

4. 如果已选择自定义权限选项，此时指定以下项：

   - **选择权限**：在保护所选文件时选择希望用户具有的访问级别。
    
   - **选择用户、组或组织**：指定应对文件具有选定权限的人员。 键入他们的完整电子邮件地址、组电子邮件地址或相应组织中所有用户的组织域名。 
    
     或者，可以使用“通讯簿”图标从 Outlook 通讯簿选择用户或组。
        
    - **过期访问**：选择此选项只对时间敏感文件，以便指定的人员无法设置日期后打开选定的文件。 仍可以打开原始文件，但在设置日期的午夜（当前时区）过后，指定的人员将无法打开该文件。
    
     请注意，如果此设置此前通过 Office 2010 应用的自定义权限配置，则指定到期日期不会显示在此对话框中，但仍然会设置到期日期。 此显示问题仅适用于在 Office 2010 中配置了到期日期的情况。

5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

根据你的选择，现已对所选择的一个或多个文件进行分类和保护。 在某些情况下（添加的保护更改了文件扩展名时），文件资源管理器中的原始文件将替换为具有 Azure 信息保护锁状图标的新文件。 例如：

![Azure 信息保护中具有锁状图标的受保护文件](../media/Pfile.png)

如果改变了有关分类和保护的想法，或稍后需要更改设置，仅需通过重复此过程进行新的设置。

指定的分类和保护会保留在文件中，即使你通过电子邮件发送文件或将其保存到其他位置也是如此。 

## <a name="other-instructions"></a>其他说明
为 Azure 信息保护统一标记客户端将指导用户从多个操作说明：

-   [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    

请参阅[概述的敏感度标签](/Office365/SecurityCompliance/sensitivity-labels)。
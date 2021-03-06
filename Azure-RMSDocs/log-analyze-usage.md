---
title: 日志 & 分析 Azure 信息保护中的保护使用情况
description: 有关如何使用 Azure 信息保护中的保护服务的使用日志记录的信息和说明。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c18c3e6524e6c42ee4b639b42778a8a8217b12d0
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136786"
---
# <a name="logging-and-analyzing-the-protection-usage-from-azure-information-protection"></a>记录和分析 Azure 信息保护中的保护使用情况

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

使用此信息来帮助你了解如何使用 Azure 信息保护中的保护服务（Azure Rights Management）的使用日志记录。 此保护服务为组织的文档和电子邮件提供数据保护，并可以记录每个请求。 这些请求包括在用户保护文档和电子邮件以及使用此内容时，管理员为该服务执行的操作，以及 Microsoft 操作员为了支持 Azure 信息保护部署而执行的操作。 

然后，你可以使用这些保护使用日志来支持以下业务方案：

-   **分析信息以获得业务见解**

    保护服务生成的日志可以导入到所选的存储库中（例如数据库、联机分析处理（OLAP）系统或地图缩减系统），以分析信息和生成报告。 例如，可以看出谁在访问受保护的数据。 还可以确定用户访问了哪些受保护的数据、从哪些设备访问、从何处访问。 你可以了解用户是否能够成功读取受保护内容。 你还可以看出哪些用户阅读了某个受保护的重要文档。

-   **监控滥用行为**

    您可以近乎实时地使用有关保护使用情况的日志记录信息，以便您可以持续监视公司对保护服务的使用情况。 99.9% 的日志可在对服务启动操作后 15 分钟之内访问。

    例如，如果在正常工作时间之外读取受保护数据的用户迅猛增加，可能意味着恶意用户正在收集信息并企图售卖给你的竞争对手，你希望在出现这种情况时收到警报。 或者，如果同一用户在很短时间内显然是从两个不同 IP 地址访问数据，则可能意味着该用户帐户已泄漏。

-   **执行取证分析**

    如果遇到信息泄露，安全人员很可能向你询问最近谁访问了特定文档，以及可疑人员最近访问了哪些信息。 使用此日志记录时，可以回答这些类型的问题，因为使用受保护内容的用户必须始终获取 Rights Management 许可证才能打开受 Azure 信息保护保护的文档和图片，即使这些文件通过电子邮件移动或复制到 USB 驱动器或其他存储设备也是如此。 这意味着，当你使用 Azure 信息保护来保护你的数据时，可以使用这些日志作为权威性的信息源进行取证分析。

除了此使用日志记录之外，还可以使用以下日志记录选项：

|日志记录选项|说明|
|----------------|---------------|
|管理员日志|记录保护服务的管理任务。 例如，在停用服务的情况下，启用超级用户功能时，以及向用户委派服务的管理员权限时。 <br /><br />有关详细信息，请参阅 PowerShell cmdlet [AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)。|
|文档跟踪|允许用户跟踪和撤消其使用 Azure 信息保护客户端跟踪的文档。 全局管理员也可以代表用户跟踪这些文档。 <br /><br />有关详细信息，请参阅[配置和使用 Azure 信息保护的文档跟踪](./rms-client/client-admin-guide-document-tracking.md)。|
|客户端事件日志|Azure 信息保护客户端的使用活动记录在本地 Windows“应用程序和服务”**** 事件日志和“Azure 信息保护”**** 中。 <br /><br />有关详细信息，请参阅 [Azure 信息保护客户端的使用日志记录](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)。|
|客户端日志文件|有关 Azure 信息保护客户端的疑难解答日志，位于 %localappdata%\Microsoft\MSIP**** 中。 <br /><br />这些文件专门设计供 Microsoft 支持部门使用。|

此外，会收集并聚合 Azure 信息保护客户端使用情况日志和 Azure 信息保护扫描程序中的信息以在 Azure 门户中创建报表。 有关详细信息，请参阅 [Azure 信息保护报表](reports-aip.md)。

使用下列部分来了解有关保护服务的使用日志记录的详细信息。 

## <a name="how-to-enable-logging-for-protection-usage"></a>如何启用保护使用日志记录
默认情况下，为所有客户启用保护使用日志记录。 

不针对日志存储或日志记录功能收取额外的费用。

## <a name="how-to-access-and-use-your-protection-usage-logs"></a>如何访问和使用保护使用日志
Azure 信息保护将日志作为一系列 blob 写入到 Azure 存储帐户，该帐户会为你的租户自动创建。 每个 Blob 包含一条或多条日志记录，采用 W3C 扩展日志格式。 Blob 名称为数字，按创建顺序排列。 本文档后面的[如何解释 Azure Rights Management 使用日志](#how-to-interpret-your-usage-logs)部分包含了有关日志内容及其创建情况的更多信息。

在保护操作之后，日志可能需要一些时间才能显示在存储帐户中。 大多数日志在 15 分钟之内显示。 我们建议你将日志下载到本地存储，例如本地文件夹、数据库或 map-reduce 存储库。

若要下载使用日志，需要使用适用于 Azure 信息保护的 AIPService PowerShell 模块。 有关安装说明，请参阅[安装 AIPService PowerShell 模块](install-powershell.md)。

### <a name="to-download-your-usage-logs-by-using-powershell"></a>使用 PowerShell 下载使用日志

1.  使用 "以**管理员身份运行**" 选项启动 Windows PowerShell，并使用[AipService](/powershell/module/aipservice/connect-aipservice) Cmdlet 连接到 Azure 信息保护：

    ```
    Connect-AipService
    ```
    
2.  运行以下命令，以下载特定日期的日志： 

    ```
    Get-AipServiceUserLog -Path <location> -fordate <date>
    ```

    例如，在 E 盘上创建名为 Logs 的文件夹之后：
    
    * 若要下载特定日期（例如 2016/2/1）的日志，请运行以下命令：`Get-AipServiceUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * 若要下载某一日期范围（例如从 2016/2/1 到 2016/2/14）的日志，请运行以下命令：`Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

如果你只指定了天（如我们的示例），则时间将假定为本地时间的 00:00:00，然后转换为 UTC。 如果你使用 -fromdate 或 -todate 参数指定了时间（例如，fordate "2/1/2016 15:00:00"），则日期和时间将转换为 UTC。 然后，AipServiceUserLog 命令获取该 UTC 时间段的日志。

你不能指定少于一整天的时间来进行下载。

默认情况下，此 cmdlet 使用三个线程来下载日志。 如果你有足够的网络带宽，并且想要减少下载日志所需的时间，可使用 -NumberOfThreads 参数，该参数支持从 1 到 32 的值。 例如，如果你运行以下命令，此 cmdlet 将生成 10 个线程来下载日志：`Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> 你可以使用 [Microsoft Log Parser](https://www.microsoft.com/download/details.aspx?id=24659)（一种在各种常见日志格式之间进行转换的工具），将所有已下载日志文件整合为 CSV 格式。 你还能够使用该工具将数据转换为 SYSLOG 格式，或者将其导入到数据库。 安装该工具之后，请运行 `LogParser.exe /?` 以获得此工具的使用帮助和信息。 
>
> 例如，你可以运行以下命令，将所有信息导出为 .log 文件格式：`logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

## <a name="how-to-interpret-your-usage-logs"></a>如何解释使用日志
使用以下信息来帮助你解释保护使用日志。

### <a name="the-log-sequence"></a>日志序列
Azure 信息保护将日志作为一系列 blob 写入。

日志中的每个条目都有 UTC 时间戳。 由于保护服务在多个数据中心的多个服务器上运行，有时日志可能看起来不是顺序的，即使它们按时间戳排序也是如此。 不过这种差异很小，通常在一分钟之内。 大多数情况下，这不会为日志分析带来麻烦。

### <a name="the-blob-format"></a>Blob 格式
所有 Blob 都采用 W3C 扩展日志格式。 开头是以下两行：

**#软件：RMS**

**#Version：1。1**

第一行标识这些是 Azure 信息保护中的保护日志。 第二行标识 Blob 的剩余部分遵循版本 1.1 规范。 我们建议，用于解析这些日志的任何应用程序都应先验证这两行，然后再继续解析 Blob 的剩余部分。

第三行枚举字段名称列表，以制表符分隔：

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

后面的每行都是日志记录。 这些字段的值与前一行具有相同的顺序，并且以制表符分隔。 请使用下表分析这些字段。


|   字段名   | W3C 数据类型 |                                                                                                                                                                          说明                                                                                                                                                                          |                                                            示例值                                                            |
|----------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
|      date      |     日期      |                                                                                                                     为请求提供服务时的 UTC 日期。<br /><br />源是为请求提供服务的服务器上的本地时钟。                                                                                                                     |                                                             2013-06-25                                                              |
|      time      |     时间      |                                                                                                            为请求提供服务时的 UTC 时间（24 小时格式）。<br /><br />源是为请求提供服务的服务器上的本地时钟。                                                                                                            |                                                              21:59:28                                                               |
|     row-id     |     文本      |                                                                           此日志记录的唯一 GUID。 如果不存在值，则使用 correlation-id 值来标识该条目。<br /><br />在你整合日志或将日志复制为其他格式时，这个值是有用的。                                                                           |                                                1c3fe7a9-d9e0-4654-97b7-14fafa72ea63                                                 |
|  request-type  |     名称      |                                                                                                                                                            所请求的 RMS API 的名称。                                                                                                                                                            |                                                           AcquireLicense                                                            |
|    user-id     |    String     |                                                               发出请求的用户。<br /><br />该值包括在单引号中。 由你管理的租户密钥 (BYOK) 所发出的调用具有值 **"**，这也适用于请求类型为匿名时的情况。                                                                |                                                          ‘joe@contoso.com’                                                          |
|     result     |    String     |                                                                                                                  如果成功地为请求提供服务，则为 ‘Success’。<br /><br />如果为请求提供服务失败，则在单引号中显示错误类型。                                                                                                                   |                                                              “Success”                                                              |
| correlation-id |     文本      |                                                                                                 在 RMS 客户端日志和服务器日志之间通用的针对给定请求的 GUID。<br /><br />此值有助于你解决客户端问题。                                                                                                 |                                                cab52088-8925-4371-be34-4b71a3112356                                                 |
|   content-id   |     文本      |                                                                      包括在大括号中的 GUID，标识受保护内容（例如某个文档）。<br /><br />只有当 request-type 为 AcquireLicense 时，此字段才具有值，对于其他所有请求类型，此字段都为空。                                                                       |                                               {bb4af47b-cfed-4719-831d-71b98191a4f2}                                                |
|  owner-email   |    String     |                                                                                                                       文档所有者的电子邮件地址。<br /><br /> 如果请求类型为 RevokeAccess，则此字段为空。                                                                                                                        |                                                          alice@contoso.com                                                          |
|     颁发者     |    String     |                                                                                                                          文档发布者的电子邮件地址。 <br /><br /> 如果请求类型为 RevokeAccess，则此字段为空。                                                                                                                          |                       alice@contoso.com（或）FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com’                       |
|  template-id   |    String     |                                                                                                                    用于保护文档的模板的 ID。 <br /><br /> 如果请求类型为 RevokeAccess，则此字段为空。                                                                                                                     |                                               {6d9371a6-4e2d-4e97-9a38-202233fed26e}                                                |
|   file-name    |    String     | 使用适用于 Windows 的 Azure 信息保护客户端跟踪的受保护文档的文件名。 <br /><br />目前，某些文件（如 Office 文档）显示为 GUID 而不是实际文件名。<br /><br /> 如果请求类型为 RevokeAccess，则此字段为空。 |                                                       TopSecretDocument.docx                                                        |
| date-published |     日期      |                                                                                                                          保护文档时的日期。<br /><br /> 如果请求类型为 RevokeAccess，则此字段为空。                                                                                                                           |                                                         2015-10-15T21:37:00                                                         |
|     c-info     |    String     |                                                                                   有关发出请求的客户端平台的信息。<br /><br />特定字符串各不相同，具体取决于应用程序（例如操作系统或浏览器）。                                                                                   | 'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64' |
|      c-ip      |    地址    |                                                                                                                                                       发出请求的客户端的 IP 地址。                                                                                                                                                        |                                                            64。51。202。144                                                            |
|  admin-action  |     Bool      |                                                                                                                                    管理员是否已在管理员模式下访问文档跟踪站点。                                                                                                                                    |                                                                True                                                                 |
| acting-as-user |    String     |                                                                                                                               管理员正在访问其文档跟踪站点的用户的电子邮件地址。                                                                                                                                |                                                          'joe@contoso.com'                                                          |

#### <a name="exceptions-for-the-user-id-field"></a>user-id 字段的例外
虽然 user-id 字段通常指示发出请求的用户，但在两种例外情况下，该值不映射到真正用户：

-   值 **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**。

    这表示 Office 365 服务（如 Exchange Online 或 Microsoft SharePoint）正在发出请求。 在字符串中， * &lt; YourTenantID &gt; *是租户的 GUID，而* &lt; 区域 &gt; *是租户注册的区域。 例如，**na** 代表北美，**eu** 代表欧洲，**ap** 代表亚洲。

-   如果你使用 RMS 连接器。

    此连接器发出的请求将使用服务主体名称 **Aadrm_S-1-7-0** 进行记录，该名称是在安装 RMS 连接器时自动生成的。

#### <a name="typical-request-types"></a>典型请求类型
保护服务有很多请求类型，但下表列出了一些最常用的请求类型。

|请求类型|说明|
|----------------|---------------|
|AcquireLicense|基于 Windows 的计算机上的客户端正在请求受保护内容的许可证。|
|AcquirePreLicense|客户端代表用户请求受保护内容的许可证。|
|AcquireTemplates|进行调用以基于模板 ID 获取模板|
|AcquireTemplateInformation|进行调用以从服务获取模板的 ID。|
|AddTemplate|从 Azure 门户进行调用以添加模板。|
|AllDocsCsv|从文档跟踪站点进行调用，以便从“所有文档”**** 页面下载 CSV 文件。|
|BECreateEndUserLicenseV1|从移动设备进行调用以创建最终用户许可证。|
|BEGetAllTemplatesV1|从移动设备（后端）进行调用以获取所有模板。|
|Certify|客户端正在认证用户对受保护内容的使用和创建情况。|
|DeleteTemplateById|从 Azure 门户进行调用以按模板 ID 删除模板。|
|DocumentEventsCsv|从文档跟踪站点进行调用，以便下载单个文档的 .CSV 文件。|
|ExportTemplateById|从 Azure 门户进行调用以基于模板 ID 导出模板。|
|FECreateEndUserLicenseV1|类似于 AcquireLicense 请求，但来自移动设备。|
|FECreatePublishingLicenseV1|与 Certify 和 GetClientLicensorCert 组合请求相同，来自移动客户端。|
|FEGetAllTemplates|从移动设备（前端）进行调用以获取模板。|
|FindServiceLocationsForUser|进行调用以查询 URL，使用该项来调用 Certify 或 AcquireLicense。|
|GetAllDocs|从文档跟踪站点进行调用，以便为用户加载“所有文档”**** 页面，或者搜索该租户的所有文档。 将此值与 admin-action 和 acting-as-admin 字段结合使用：<br /><br />- admin-action 为空：用户在“所有文档”**** 页面中查看自己的文档。<br /><br />- admin-action 为 true 且 acting-as-user 为空：管理员查看其租户的所有文档。<br /><br />- admin-action 为 true 且 acting-as-user 不为空：管理员查看用户的“所有文档”**** 页面。|
|GetAllTemplates|从 Azure 门户进行调用以获取所有模板。|
|GetClientLicensorCert|客户端正在从基于 Windows 的计算机请求发布证书（随后用于保护内容）。|
|GetConfiguration|调用 Azure PowerShell cmdlet 以获取 Azure RMS 租户的配置。|
|GetConnectorAuthorizations|从 RMS 连接器进行调用以从云中获取其配置。|
|GetRecipients|从文档跟踪站点进行调用，以便导航到单个文档的列表视图。|
|GetSingle|从文档跟踪站点进行调用，以便导航到“单个文档”**** 页面。|
|GetTenantFunctionalState|Azure 门户正在检查是否已激活保护服务（Azure Rights Management）。|
|GetTemplateById|从 Azure 门户进行调用以通过指定模板 ID 来获取模板。|
|KeyVaultDecryptRequest|客户端正在尝试解密受 RMS 保护的内容。 仅适用于 Azure 密钥保管库中客户托管的租户密钥 (BYOK)。|
|KeyVaultGetKeyInfoRequest|进行调用以验证指定用在 Azure 信息保护租户密钥的 Azure 密钥保管库中的密钥可访问，并且未使用。|
|KeyVaultSignDigest|在将 Azure 密钥保管库中客户托管的密钥 (BYOK) 用于签名时进行调用。 通常是针对每个 AcquireLicence（或 FECreateEndUserLicenseV1）、Certify 和 GetClientLicensorCert（或 FECreatePublishingLicenseV1）请求调用一次此项。|
|KMSPDecrypt|客户端正在尝试解密受 RMS 保护的内容。 仅适用于旧版客户托管的租户密钥 (BYOK)。|
|KMSPSignDigest|在将旧版客户托管的密钥 (BYOK) 用于签名时进行调用。 通常是针对每个 AcquireLicence（或 FECreateEndUserLicenseV1）、Certify 和 GetClientLicensorCert（或 FECreatePublishingLicenseV1）请求调用一次此项。|
|LoadEventsForMap|从文档跟踪站点进行调用，以便导航到单个文档的映射视图。|
|LoadEventsForSummary|从文档跟踪站点进行调用，以便导航到单个文档的时间线视图。|
|LoadEventsForTimeline|从文档跟踪站点进行调用，以便导航到单个文档的映射视图。|
|ImportTemplate|从 Azure 门户进行调用以导入模板。|
|RevokeAccess|从文档跟踪站点进行调用以撤销文档。|
|SearchUsers |从文档跟踪站点进行调用，以便搜索某个租户中的所有用户。|
|ServerCertify|从已启用 RMS 的客户端（如 SharePoint）进行调用以认证服务器。|
|SetUsageLogFeatureState|进行调用以启用使用日志记录。|
|SetUsageLogStorageAccount|进行调用以指定 Azure Rights Management 服务日志的位置。|
|UpdateNotificationSettings|从文档跟踪站点进行调用，以便更改单个文档的通知设置。|
|UpdateTemplate|从 Azure 门户进行调用以更新现有模板。|


## <a name="powershell-reference"></a>PowerShell 参考

访问保护使用日志记录所需的唯一 PowerShell cmdlet 是[AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)。 

有关使用 PowerShell 进行 Azure 信息保护的详细信息，请参阅[使用 Powershell 管理 Azure 信息保护中的保护](administer-powershell.md)。

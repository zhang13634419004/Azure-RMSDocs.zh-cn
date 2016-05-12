---
# required metadata

title: 记录和分析 Azure Rights Management 使用情况 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 记录和分析 Azure Rights Management 使用情况
本主题中的信息可用于帮助你了解如何使用 Azure Rights Management (Azure RMS) 的使用日志记录功能。 Azure Rights Management 服务能够记录它为你组织发出的所有请求，包括来自用户的请求、你组织中的 Rights Management 管理员执行的操作、Microsoft 操作人员为支持 Azure Rights Management 部署而执行的操作。

然后，你可以使用这些 Azure Rights Management 日志来支持以下业务方案：

-   **分析信息以获得业务见解**

    可将 Azure Rights Management 生成的日志导入到你选择的存储库（例如数据库、联机分析处理 (OLAP) 系统或 map-reduce 系统），以便分析信息并生成报告。 例如，你可以看出谁在访问你的 RMS 保护数据。 你还可以确定用户访问了哪些 RMS 保护数据、从哪些设备访问、从何处访问。 你可以了解用户是否能够成功读取受保护内容。 你还可以看出哪些用户阅读了某个受保护的重要文档。

-   **监控滥用行为**

    你可以近乎实时地访问 Azure Rights Management 日志记录信息，从而持续监控你公司使用 Rights Management 的情况。 99.9% 的日志可在 RMS 启动操作后 15 分钟之内访问。

    例如，如果在正常工作时间之外读取 RMS 保护数据的用户迅猛增加，可能意味着恶意用户正在收集信息并企图售卖给你的竞争对手，你希望在出现这种情况时收到警报。 或者，如果同一用户在很短时间内显然是从两个不同 IP 地址访问数据，则可能意味着该用户帐户已泄漏。

-   **执行取证分析**

    如果遇到信息泄露，安全人员很可能向你询问最近谁访问了特定文档，以及可疑人员最近访问了哪些信息。 当你使用 Azure Rights Management 和日志记录时，你就能够回答这些类型的问题，因为使用受保护内容的用户始终必须获取 Rights Management 许可证才能打开受 Azure Rights Management 保护的文档和图片，即便这些文件已移动（通过电子邮件）或复制到 U 盘/其他存储设备也是如此。 这意味着在通过 Azure Rights Management 保护数据时，你能够使用 Azure Rights Management 日志作为确定性信息源进行取证分析。

> [!NOTE]
> 如果你只希望记录 Azure Rights Management 的管理任务，而不希望跟踪用户如何使用 Rights Management，则可使用适用于 Azure Rights Management 的 [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) Windows PowerShell cmdlet。
> 
> 你还可以使用 Azure 经典门户获取高级使用情况报告，包括“RMS 摘要”、“RMS 活动用户”、“RMS 设备平台”和“RMS 应用程序使用情况”****************。 若要从 Azure 经典门户访问这些报告，请单击“Active Directory”，选择并打开一个目录，然后单击“报告”********。

有关 Azure Rights Management 使用日志记录的详细信息，请参阅以下部分。

## 如何启用 Azure Rights Management 使用日志记录
从 2016 年 2 月开始，Azure Rights Management 使用日志记录功能默认为对所有用户启用。 这适用于在 2016 年 2 月以前已激活其 Azure RMS 服务的客户和在 2016 年 2 月后激活该服务的客户。 

> [!NOTE]
> 不针对日志存储或日志记录功能收取额外的费用。
> 
> 如果你在 2016 年 2 月以前使用 Azure RMS 的使用日志记录，你需要在 Azure 上拥有订阅和足够的存储空间，而现在不再需要如此。



## 如何访问和使用 Azure Rights Management 使用日志
Azure Rights Management 将日志作为一系列 Blob 写入你的 Azure 存储帐户。 每个 Blob 包含一条或多条日志记录，采用 W3C 扩展日志格式。 Blob 名称为数字，按创建顺序排列。 本文档后面的[如何解释 Azure Rights Management 使用日志](#how-to-interpret-your-azure-rights-management-usage-logs)部分包含了有关日志内容及其创建情况的更多信息。

在 Azure Rights Management 操作之后，日志需要一段时间才能显示在你的存储帐户中。 大多数日志在 15 分钟之内显示。 我们建议你将日志下载到本地存储，例如本地文件夹、数据库或 map-reduce 存储库。

若要下载使用日志，可使用适用于 Windows PowerShell 的 Azure RMS 管理模块。 有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。 如果你之前已下载了此 Windows PowerShell 模块，请运行以下命令来检查你的版本号是否至少为 **2.4.0.0**： `(Get-Module aadrm -ListAvailable).Version` 

### 使用 PowerShell 下载使用日志

1.  使用“以管理员身份运行”****选项启动 Windows PowerShell，然后使用 [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) cmdlet 连接到 Azure Rights Management 服务：

    ```
    Connect-AadrmService
    ```
    
2.  运行以下命令，以下载特定日期的日志： 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    例如，在 E 盘上创建名为 Logs 的文件夹之后：
    
    * 若要下载特定日期（例如 2016/2/1）的日志，请运行以下命令： `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * 若要下载某一日期范围（例如从 2016/2/1 到 2016/2/14）的日志，请运行以下命令： `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

如果你只指定了天（如我们的示例），则时间将假定为本地时间的 00:00:00，然后转换为 UTC。 如果你使用 -fromdate 或 -todate 参数指定了时间（例如，fordate "2/1/2016 15:00:00"），则日期和时间将转换为 UTC。 然后，Get-AadrmUserLog 命令将获取该 UTC 时间段的日志。

你不能指定少于一整天的时间来进行下载。

默认情况下，此 cmdlet 使用三个线程来下载日志。 如果你有足够的网络带宽，并且想要减少下载日志所需的时间，可使用 -NumberOfThreads 参数，该参数支持从 1 到 32 的值。 例如，如果你运行以下命令，此 cmdlet 将生成 10 个线程来下载日志： `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> 你可以使用 [Microsoft Log Parser](https://www.microsoft.com/download/details.aspx?id=24659)（一种在各种常见日志格式之间进行转换的工具），将所有已下载日志文件整合为 CSV 格式。 你还能够使用该工具将数据转换为 SYSLOG 格式，或者将其导入到数据库。 安装该工具之后，请运行 `LogParser.exe /?` 以获得此工具的使用帮助和信息。 
>
> 例如，你可以运行以下命令，将所有信息导出为 .log 文件格式： `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### 如果你已在 2016 年 2 月 22 日日志记录更改之前手动启用 Azure RMS 使用日志记录


如果你在日志记录更改之前已使用使用日志记录，你将会在已配置的 Azure 存储帐户中找到使用日志。 Microsoft 不会将这些日志从你的存储帐户复制到新的 Azure RMS 管理的存储帐户作为此日志记录更改的一部分。 你负责管理以前生成的日志的生命周期，并可以使用 [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) cmdlet 来下载旧日志。 例如：

- 将所有可用日志下载到 E:\logs 文件夹： `Get-AadrmUsageLog -Path "E:\Logs"`
    
- 下载特定范围的 Blob： `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

请注意，如果以下任一情况适用，则无需使用 Get-AadrmUsageLog cmdlet 来下载日志：

-  你已在 2016 年 2 月 22 日当天或之前激活 Azure Rights Management，但未启用使用日志记录功能。

- 你已在 2016 年 2 月 22 日之后激活 Azure Rights Management。

## 如何解释 Azure Rights Management 使用日志
使用以下信息可帮助你解释 Azure Rights Management 使用日志。

### 日志序列
Azure Rights Management 将日志作为一系列 Blob 写入。 

日志中的每个条目都有 UTC 时间戳。 由于 Azure Rights Management 在跨多个数据中心的多个服务器上运行，有时日志即使是按时间戳排序，也似乎并不符合时间顺序。 不过这种差异很小，通常在一分钟之内。 大多数情况下，这不会为日志分析带来麻烦。

### Blob 格式
所有 Blob 都采用 W3C 扩展日志格式。 开头是以下两行：

**#软件：RMS**

**#版本：1.1**

第一行标识这些是 Azure Rights Management 日志。 第二行标识 Blob 的剩余部分遵循版本 1.1 规范。 我们建议，用于解析这些日志的任何应用程序都应先验证这两行，然后再继续解析 Blob 的剩余部分。

第三行枚举字段名称列表，以制表符分隔：

**#字段：date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

后面的每行都是日志记录。 这些字段的值与前一行具有相同的顺序，并且以制表符分隔。 请使用下表分析这些字段。

|字段名称|W3C 数据类型|说明|示例值|
|--------------|-----------------|---------------|-----------------|
|date|日期|为请求提供服务时的 UTC 日期。<br /><br />源是为请求提供服务的服务器上的本地时钟。|2013-06-25|
|time|时间|为请求提供服务时的 UTC 时间（24 小时格式）。<br /><br />源是为请求提供服务的服务器上的本地时钟。|21:59:28|
|row-id|文本|此日志记录的唯一 GUID。<br /><br />在你整合日志或将日志复制为其他格式时，这个值是有用的。|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Name|所请求的 RMS API 的名称。|AcquireLicense|
|user-id|String|发出请求的用户。<br /><br />该值包括在单引号中。 有些请求类型是匿名的，在这种情况下，该值为 ”。|‘joe@contoso。com’|
|result|String|如果成功地为请求提供服务，则为‘Success’。<br /><br />如果为请求提供服务失败，则在单引号中显示错误类型。|‘Success’|
|correlation-id|文本|在 RMS 客户端日志和服务器日志之间通用的针对给定请求的 GUID。<br /><br />此值有助于你解决客户端问题。|cab52088-8925-4371-be34-4b71a3112356|
|content-id|文本|包括在大括号中的 GUID，标识受保护内容（例如某个文档）。<br /><br />只有当 request-type 为 AcquireLicense 时，此字段才具有值，对于其他所有请求类型，此字段都为空。|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|String|文档所有者的电子邮件地址。|alice@contoso.com|
|issuer|String|文档发布者的电子邮件地址。|alice@contoso.com（或）FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Template-id|String|用于保护文档的模板的 ID。|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|File-name|String|已保护的文档的文件名。|TopSecretDocument.docx|
|Date-published|日期|保护文档时的日期。|2015-10-15T21:37:00|
|c-info|String|有关发出请求的客户端平台的信息。<br /><br />特定字符串各不相同，具体取决于应用程序（例如操作系统或浏览器）。|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Address|发出请求的客户端的 IP 地址。|64.51.202.144|

#### user-id 字段的例外
虽然 user-id 字段通常指示发出请求的用户，但在两种例外情况下，该值不映射到真正用户：

-   值 **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**。

    它指示 Office 365 服务（例如 Exchange Online 或 Sharepoint Online）正在发出请求。 在字符串中， *&lt;YourTenantID&gt;* 是你租户的 GUID， *&lt;region&gt;* 是你租户注册的区域。 例如， **na** 代表北美， **eu** 代表欧洲， **ap** 代表亚洲。

-   如果你使用 RMS 连接器。

    此连接器发出的请求将使用服务主体名称来进行记录，该名称是 RMS 在你安装 RMS 连接器时自动生成的。

#### 典型请求类型
Azure Rights Management 中有很多请求类型，但下表列出了其中一些最常用的请求类型。

|请求类型|说明|
|----------------|---------------|
|AcquireLicense|基于 Windows 的计算机上的客户端为受 RMS 保护的内容请求许可证。|
|AcquirePreLicense|客户端代表用户为受 RMS 保护的内容请求许可证。|
|AcquireTemplates|进行调用以基于模板 ID 获取模板|
|AcquireTemplateInformation|进行调用以从服务获取模板的 ID。|
|AddTemplate|从 Azure 经典门户进行调用以添加模板。|
|BECreateEndUserLicenseV1|从移动设备进行调用以创建最终用户许可证。|
|BEGetAllTemplatesV1|从移动设备（后端）进行调用以获取所有模板。|
|Certify|客户端正在认证要保护的内容。|
|Decrypt|客户端正在尝试解密受 RMS 保护的内容。|
|DeleteTemplateById|从 Azure 经典门户进行调用以按模板 ID 删除模板。|
|ExportTemplateById|从 Azure 经典门户进行调用以基于模板 ID 导出模板。|
|FECreateEndUserLicenseV1|类似于 AcquireLicense 请求，但来自移动设备。|
|FECreatePublishingLicenseV1|与 Certify 和 GetClientLicensorCert 组合请求相同，来自移动客户端。|
|FEGetAllTemplates|从移动设备（前端）进行调用以获取模板。|
|GetAllTemplates|从 Azure 经典门户进行调用以获取所有模板。|
|GetClientLicensorCert|客户端正在从基于 Windows 的计算机请求发布证书（随后用于保护内容）。|
|GetConfiguration|调用 Azure PowerShell cmdlet 以获取 Azure RMS 租户的配置。|
|GetConnectorAuthorizations|从 RMS 连接器进行调用以从云中获取其配置。|
|GetTenantFunctionalState|Azure 经典门户检查是否已激活 Azure RMS。|
|GetTemplateById|从 Azure 经典门户进行调用以通过指定模板 ID 来获取模板。|
|ExportTemplateById|从 Azure 经典门户进行调用以通过指定模板 ID 来导出模板。|
|FindServiceLocationsForUser|进行调用以查询 URL，使用该项来调用 Certify 或 AcquireLicense。|
|ImportTemplate|从 Azure 经典门户进行调用以导入模板。|
|ServerCertify|从已启用 RMS 的客户端（如 SharePoint）进行调用以认证服务器。|
|SetUsageLogFeatureState|进行调用以启用使用日志记录。|
|SetUsageLogStorageAccount|进行调用以指定 Azure RMS 日志的位置。|
|SignDigest|在密钥用于签名目的时进行调用。 通常是针对每个 AcquireLicence（或 FECreateEndUserLicenseV1）、Certify 和 GetClientLicensorCert（或 FECreatePublishingLicenseV1）请求调用一次此项。|
|UpdateTemplate|从 Azure 经典门户进行调用以更新现有模板。|

## Windows PowerShell 参考
从 2016 年 2 月起，Azure RMS 使用日志记录需要的唯一 Windows PowerShell cmdlet 为 [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)。 

在此更改之前，Azure RMS 使用日志需要以下 cmdlet（现已弃用）：  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

如果你在 Azure RMS 日志记录更改之前在自己的 Azure 存储空间中保存了日志，可以像以前一样使用这些较旧的 cmdlet（如使用 Get-AadrmUsageLog 和Get-AadrmUsageLogLastCounterValue）下载这些日志。 但所有新的使用日志将写入到新的 Azure RMS 存储空间，并且必须使用 Get-AadrmUserLog 下载。

若要深入了解适用于 Azure Rights Management 的 Windows PowerShell，请参阅[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)。





<!--HONumber=Apr16_HO3-->


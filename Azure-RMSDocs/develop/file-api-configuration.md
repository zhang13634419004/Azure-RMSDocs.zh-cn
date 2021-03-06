---
title: 文件 API 配置 |Azure RMS
description: 可通过注册表中的设置来配置文件 API 的行为。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 10/11/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 673a23afa25872981967b48f81397d4a742855a8
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135617"
---
# <a name="file-api-configuration"></a>文件 API 配置


可通过注册表中的设置来配置文件 API 的行为。

文件 API 提供两种类型的保护：本机保护和 PFile 保护。

-   **本机保护** -文件基于其 MIME 类型（文件扩展名）使用 AD RMS 格式得到保护。
-   **PFile 保护** - 文件使用 AD RMS 保护文件 (PFile) 格式得到保护。

有关受支持的文件格式的详细信息，请参阅本文中的“文件 API 文件支持详细信息”****。

## <a name="keykey-value-types-and-descriptions"></a>密钥/密钥值类型和描述

以下各节描述了控制加密的密钥和密钥值。

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection`

**类型**：密钥

**描述**：包含文件 API 的常规配置。

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>`

**类型**：密钥

**描述**：指定特定文件扩展名的配置信息;例如，TXT、JPG 等。

- 允许使用通配符“*”，但是，特定扩展名的设置优先于通配符设置。 通配符不会影响 Microsoft Office 文件的设置；必须按文件类型显式禁用这些设置。
- 若要指定没有扩展名的文件，请使用“.”
- 指定特定文件扩展名的密钥时请勿指定“.”字符；例如，使用 `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` 来指定.txt 文件的设置。 （请勿使用 `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`）。

要指定保护行为，请在密钥中设置“Encryption”值****。 如果未设置**加密**值，则会观察到该文件类型的默认行为。


### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>\Encryption*`

**类型**： REG_SZ

**描述**：包含以下三个值之一：

- **Off**：加密处于禁用状态。

> [!Note]
> 此设置对解密没有任何影响。 任何加密文件（无论是使用本机保护还是 .Pfile 保护进行加密）只要用户具有**提取**权限，就可以对其进行解密。

- **Native**：使用本机加密。 对于 Office 文件，加密文件将具有与原始文件相同的扩展名。 例如，文件扩展名为 .docx 的文件将被加密为扩展名为 .docx 的文件。 对于其他可以应用本机保护的文件，会将文件加密为具有 p*zzz* 扩展名格式的文件，其中 *zzz* 是原始文件扩展名。 例如，.txt 文件会被加密为扩展名为 .ptxt 的文件。 下面是可应用本机保护的文件扩展名列表。

- **Pfile**：使用 PFile 加密。 加密的文件会将 .pfile 追加到原来的扩展名。 例如，加密后，.txt 文件的文件扩展名将为 .txt.pfile。


> [!Note]
> 此设置对于 Office 文件格式没有任何影响。 例如，如果将 `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` 值设置为 ".pfile"，则将仍使用本机保护来加密 .docx 文件，并且加密文件的文件扩展名为 .docx。

设置任何其他值或不设置任何值将导致默认行为。

## <a name="default-behavior-for-different-file-formats"></a>不同文件格式的默认行为

-   **Office 文件** 启用了本机加密。
-   **txt、xml、jpg、jpeg、pdf、png、tiff、bmp、gif、giff、jpe、jfif、jif 文件** 启用了本机加密（xxx 变成 pxxx）
-   **所有其他文件** 启用了加密即受保护文件 (pfile)（xxx 变成 pxxx）

如果对阻止的文件类型尝试加密，则会出现 [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx) 错误。

### <a name="file-api---file-support-details"></a>文件 API - 文件支持详细信息

可为任何文件类型（扩展名）添加本机支持。 例如，对于任何扩展 &lt;ext&gt;（非 office），如果该扩展的管理配置是“NATIVE”，则将使用 \*.p&lt;ext&gt;。

**Office 文件**

-   文件扩展名：doc、dot、xla、xls、xlt、pps、ppt、docm、docx、dotm、dotx、xlam、xlsb、xlsm、xlsx、xltm、xltx、xps、potm、potx、ppsx、ppsm、pptm、pptx、thmx、vsdx、vsdm、vssx、vssm、vstx 和 vstm。 
-   保护类型 = Native（默认）：sample.docx 加密为 sample.docx
-   保护类型 = Pfile：对于 Office 文件，具有与 Native 相同的效果。
-   Off：禁用加密。

**PDF 文件**

-   保护类型 = Native：sample.pdf 被加密，并命名为 sample.ppdf
-   保护类型 = Pfile：sample.pdf 被加密，并命名为 sample.pdf.pfile。
-   Off：禁用加密。

**所有其他文件格式**

-   保护类型 = .Pfile： sample。*zzz*经过加密和命名示例。*zzz*.pfile;其中， *zzz*是原始文件扩展名。
-   Off：禁用加密。

### <a name="examples"></a>示例

以下设置为 txt 文件启用了 PFile 加密。 Office 文件将应用本机保护（默认），txt 文件将应用 PFile 保护，所有其他文件都将阻止保护（默认）。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

以下设置为所有非 Office 文件（txt 文件除外）启用 PFile 加密。 Office 文件将应用本机保护（默认），txt 文件将阻止保护，所有其他文件将应用 PFile 保护。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

以下设置对 docx 文件禁用本机加密。 Office 文件（docx 文件除外）将应用本机保护（默认），所有其他文件都将阻止保护（默认）。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## <a name="related-articles"></a>相关文章

- [开发人员注意事项](developer-notes.md)
- [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx)

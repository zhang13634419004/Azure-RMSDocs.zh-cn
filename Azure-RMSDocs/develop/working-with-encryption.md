---
title: 如何使用加密设置 | Azure RMS
description: Azure RMS 加密包及其使用的代码片段的方向。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 0caabd18ef06af0daaff44e8829b3bd9750a788b
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68791933"
---
# <a name="how-to-work-with-encryption-settings"></a>操作说明：使用加密设置

本主题将针对加密包，并显示其使用的一些代码段。

## <a name="support-for-aes-256-the-new-default"></a>新的默认 AES 256 的支持

假设针对 RMS SDK 2.1 2015 年 3 月的更新版本或更高版本进行构建，则无需其他代码即可使用基于的 *AES 256* 的加密，因为它是新的默认值。 应该认真考虑使用 *AES 256* 此版本的其他安全优势来更新你的应用程序。

> [!IMPORTANT]
> 对 *AES 256* 受保护的文件的使用支持自 [2014 年 10 月的版本](release-notes-rtm.md)起已存在。 如果正在运行使用 2014 年 10 月之前的 SDK 版本构建的应用程序，此更新将中断该应用程序。 请确保正在构建的应用程序的客户使用更新后的 SDK，或愿意立即更新该应用程序的最新版本。

 
## <a name="api-encryption-support"></a>API 加密支持

从 [2015 年 3 月更新](release-notes-rtm.md)开始，我们已经将下列三个标记合并到我们的 API 及其关联的加密包中：

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB（也称为不推荐使用的算法）

加密包标记（请参阅[首选加密](https://msdn.microsoft.com/library/dn974065.aspx)）可与许可证属性标记 *IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE* 结合使用。

以下是一些简单的代码段，用于演示如何使用新的许可证属性。

## <a name="deprecated-algorithms"></a>不推荐使用的算法

我们将不再公开 API 中的 *IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS* 标志。 这意味着，如果以后的应用程序引用此标记，则这些应用程序将无法再编译，但已使用它构建的应用程序可以继续工作，因为我们遵循 API 代码中的专用标记。

只需通过更改一个标记便可利用旧的不推荐使用的加密算法标记的益处。 请参阅下面的代码段示例。

## <a name="protect-files-with-aes-256-cbc4k"></a>使用 AES 256 CBC4K 保护文件

不需要代码中的更改，*AES 256* CBC4K 是默认值。

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## <a name="protect-files-with-aes-128-cbc4k"></a>使用 AES-128 CBC4K 保护文件

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## <a name="protect-files-with-aes-128-ecb-deprecated-algorithms"></a>使用 AES-128 ECB（不推荐使用的算法）保护文件

此示例还演示支持*不推荐使用的算法*的新方法。

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


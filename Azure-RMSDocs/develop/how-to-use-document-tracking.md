---
title: 如何使用文档跟踪 | Azure RMS
description: 文档跟踪功能需要对管理关联元数据以及向服务注册有一些简单了解。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: c29dd3c364cdc1df506494819e5d0b5abe1f5454
ms.sourcegitcommit: 5390bd1e0e4851b81a59094e80202f0761b7810f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80068505"
---
# <a name="how-to-use-document-tracking"></a>如何：使用文档跟踪

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

使用文档跟踪功能需要对管理关联元数据以及向服务注册有一些简单了解。

## <a name="managing-document-tracking-metadata"></a>管理文档跟踪元数据

支持文档跟踪的每个操作系统都具有类似实现。 这包括一组表示元数据的属性、一个添加到用户策略创建方法的新参数以及一个用于向文档跟踪服务注册要跟踪的策略的方法。

在操作上，只有 **内容名称** 和 **通知类型** 属性对于文档跟踪是必需的。

用于为给定的一段内容设置文档跟踪的步骤序列是：

- 创建“许可证元数据”对象，然后设置“内容名称”和“通知类型”。 这些是唯一的必需属性。
  - Android - [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx)
  -  iOS - [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx)

选择照策略类型；模板或临时：
- 对于基于模板的文档跟踪，创建 **用户策略** 对象（将许可证元数据作为参数进行传递）。
  - Android - [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx)

- 对于基于临时的文档跟踪，对 **策略描述符** 对象设置 **许可证元数据** 属性。
  - Android - [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx)
  - iOS - [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx)。

    请注意**只能在针对给定用户策略设置文档跟踪的过程中直接访问许可证元数据对象**  。 创建用户策略对象之后，无法访问关联许可证元数据，即更改许可证元数据的值会不起作用。

     

- 最后，调用文档跟踪的平台注册方法
  - Android - [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) 或 [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx)
  - iOS - [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx)

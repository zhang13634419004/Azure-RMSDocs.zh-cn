---
title: 概念 - 分类标签
description: 本文将帮助你了解如何使用标签进行数据分类。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: b2be24e1703d4831a95feaa51012cf7469a481b7
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556208"
---
# <a name="microsoft-information-protection-sdk---classification-label-concepts"></a>Microsoft 信息保护 SDK - 分类标签概念

作为全面数据保护战略的一部分，组织应实施数据分类系统来概述组织内数据的敏感程度，然后向这些分类映射文档属性。

如果该文档或数据丢失或被意外的使用者看到，则与分类相关的属性通常会给组织带来**风险**。 在为大众所熟知的美国政府分类系统中，一共有三个分类级别。 每个级别都有一个定义，描述了何时应该应用该分类：

* **最高机密**：应该应用于信息，可合理地预期未经授权泄漏该信息的行为会对原始分类机构能够识别或描述的国家/地区安全造成特别严重的损害。
* **机密**：应该应用于信息，可合理地预期未经授权泄漏该信息的行为会对原始分类机构能够识别或描述的国家/地区安全造成严重损害。
* **保密**：应该应用于信息，可合理地预期未经授权泄漏该信息的行为会对原始分类机构能够识别或描述的国家/地区安全造成损害。
* **未分类**：这实际上不是一种分类，而是指未归入以上三个级别之一。

在商业或私营部门应用程序中，我们可以定义一个列表，类似于 Azure 信息保护服务中的默认列表，并附加货币值。

* **高度保密**：应该应用于信息，可合理地预期未经授权泄漏该信息的行为会导致超过 100 万美元的损失。
* **保密**：应该应用于信息，可合理地预期未经授权泄漏该信息的行为会导致超过 10 万美元的损失。
* **常规**：应该应用于信息，可合理地预期未经授权泄漏该信息的行为会导致较轻微的损失。
* **公开**：应该应用于面向公众、供外部使用的信息。 
* **非商业性**：应该应用于与公司业务无直接或间接关系的信息。

每个分类描述了在未经授权泄漏该信息的情况下对企业造成的风险。 在确定这些分类和条件后，应确定属性，以帮助数据所有者了解要应用的分类。

## <a name="labeling"></a>添加标签

将数据分类与一组信息相关联的行为称为**添加标签**。 由于 MIP SDK 正在向文档应用分类**标签**，因此我们所指的不是分类，而是标签。 某个用户或流程已根据对信息的了解对数据进行了**分类**：MIP SDK 随后将**标记**信息。

## <a name="labels-in-the-mip-sdk"></a>MIP SDK 中的标签

标签是 MIP SDK 的基本组件。 标签用于对 SDK 触及的所有文档进行标记、保护和内容标记。 SDK 可以：

* 向文档应用标签
* 读取文档上的现有标签
* 在策略要求下更改现有标签并强制说明理由
* 从文档中删除标签

标签将根据标签管理员在安全与合规中心定义的配置应用保护和内容标记。 

## <a name="miplabel-vs-mipcontentlabel"></a>mip::Label vs. mip::ContentLabel

MIP SDK 中存在两种标签。 `Label` 和 `ContentLabel`。

* Label：可由组织策略中定义的用户或流程应用的标签。
* ContentLabel：文档或信息中已存在的标签。 可对其进行读取、更新或删除。 

换而言之，`ContentLabel` 是已应用于某条信息的 `Label`。

## <a name="metadata"></a>元数据

SDK 还支持以键/值对的形式向文档添加额外的元数据。 如果组织具有以更具体的方式描述信息的子分类或标记，则可以使用 SDK 应用该元数据。

## <a name="next-steps"></a>后续步骤

有关美国政府分类系统的更多详细信息，请参阅 https://www.gpo.gov/fdsys/pkg/FR-2010-01-05/html/E9-31418.htm 。

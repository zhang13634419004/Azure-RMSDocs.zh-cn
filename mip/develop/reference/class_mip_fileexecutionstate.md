---
title: 类 mip::FileExecutionState
description: 记录 mip::fileexecutionstate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 380e5f6732a2662d83b9bb37af5763ef30ffa3bf
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259212"
---
# <a name="class-mipfileexecutionstate"></a>类 mip::FileExecutionState 
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 std:: map\<std:: string、 std:: shared_ptr\<ClassificationResult\> \> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &、 const std:: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) 常量  |  返回分类结果的映射。
公共虚拟 std:: vector\<uint8_t\> GetSerializedProtectionInfo() 常量  |  返回具有序列化计的缓冲区
  
## <a name="members"></a>成員
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **fileHandler**:-使用的文件的文件处理程序 


* **classificationIds**： 分类 Id 的列表。 



  
**返回**:分类结果的列表。
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
返回具有序列化计的缓冲区

  
**返回**:具有序列化计的缓冲区
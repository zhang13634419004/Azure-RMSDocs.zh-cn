---
title: 类 ComputeEngine
description: 记录 Microsoft 信息保护（MIP） SDK 的 computeengine：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3b33c9a91f40422c29282ddee9292f6bbbad90c9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763502"
---
# <a name="class-computeengine"></a>类 ComputeEngine 
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<std：： shared_ptr\<标签\> \>& ListSensitivityLabels （）  | _尚无记录。_
public std：： shared_ptr\<ContentLabel\> GetSensitivityLabel （ComputeEngineContext& context，const DocumentState& state）  | _尚无记录。_
public std：： vector\<std：： shared_ptr\<Action\> \> ComputeActions （ComputeEngineContext& context，const DocumentState& DocumentState，const ApplicationActionState& actionState）  | _尚无记录。_
public std：:p air\<std：： vector\<std：： shared_ptr\<Action\>\>、bool\> ComputeActionsWithRemoteState （ComputeEngineContext& context、const DocumentState& localDocumentState、const DocumentState& remoteDocumentState、const ApplicationActionState& actionState）  |  在远程状态和本地状态之间进行选择时计算操作。
public void NotifyCommittedActions （ComputeEngineContext& context，const DocumentState& documentState，const ApplicationActionState& actionState）  | _尚无记录。_
public const std：： shared_ptr\<标签\>& GetDefaultLabel （） const  | _尚无记录。_
public const std::string& GetMoreInfoUrl() const  | _尚无记录。_
public virtual ~ ComputeEngine （）  | _尚无记录。_
  
## <a name="members"></a>成员
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
_尚无记录。_

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 函数
_尚无记录。_

  
### <a name="computeactions-function"></a>ComputeActions 函数
_尚无记录。_

  
### <a name="computeactionswithremotestate-function"></a>ComputeActionsWithRemoteState 函数
在远程状态和本地状态之间进行选择时计算操作。
使用此优先级选择状态。 未知保护类型，（模板或临时不在策略中）。 保护状态始终优于 "未保护" 状态。 带有标签的文档状态在没有的情况下优先。 推荐的标签顺序越高。 标签时间戳，喜欢最新的标记文档。 [DocumentState](class_mip_documentstate.md)LastModifiedTime （可选），首选新修改的文件。

参数：  
* **上下文**：计算机引擎上下文。 


* **localDocumentState**：本地文档状态。 


* **remoteDocumentState**：远程文档状态。 


* **actionState**：应用程序的操作状态。



  
**返回**：方法返回成对。 首先包含操作的列表，第二个操作是应在本地应用的操作，如果应在远程文档上应用错误操作并且应使用文档状态，则为。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 函数
_尚无记录。_

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel 函数
_尚无记录。_

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
_尚无记录。_

  
### <a name="computeengine-function"></a>~ ComputeEngine 函数
_尚无记录。_

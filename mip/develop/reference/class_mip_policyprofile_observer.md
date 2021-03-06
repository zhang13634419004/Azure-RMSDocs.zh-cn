---
title: 类 PolicyProfile：：观察程序
description: 记录 Microsoft 信息保护（MIP） SDK 的 policyprofile：：观察者类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 5fc8dab4c74b613ff199d16c7b39205476b87249
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760610"
---
# <a name="class-policyprofileobserver"></a>类 PolicyProfile：：观察程序 
Observer 接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 mip::Error。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess （const std：： shared_ptr\<PolicyProfile\>& profile，const std：： shared_ptr\<void\>& 上下文）  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess （const std：： vector\<std：： String\>& engineIds，const std：： shared_ptr\<void\>& 上下文）  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess （const std：： shared_ptr\<void\>& context）  |  在成功卸载引擎时调用。
public virtual void OnUnloadEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess （const std：： shared_ptr\<PolicyEngine\>& engine，const std：： shared_ptr\<void\>& 上下文）  |  在成功添加新引擎时调用。
public virtual void OnAddEngineStarting （bool requiresPolicyFetch）  |  在创建引擎之前调用，用于描述是否必须从服务器中提取引擎的策略数据，或者是否可以从本地缓存的数据中创建它。
public virtual void OnAddEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess （const std：： shared_ptr\<void\>& context）  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在删除引擎引发错误时调用。
public virtual void OnPolicyChanged(const std::string& engineId)  |  当具有给定 ID 的引擎的策略发生更改时，或在已加载的自定义敏感性类型发生更改时调用。
  
## <a name="members"></a>成员
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。

参数：  
* **profile**：用于启动操作的当前配置文件。 


* **上下文**：传递到 LoadAsync 操作的上下文。


  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。

参数：  
* error****：导致负载操作失败的错误。 


* **上下文**：传递到 LoadAsync 操作的上下文。


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 id 列表。 


* **上下文**：传递到 ListEnginesAsync 操作的上下文。


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎引发错误时调用。

参数：  
* error****：导致列出引擎操作失败的错误。 


* **上下文**：传递到 ListEnginesAsync 操作的上下文。


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess 函数
在成功卸载引擎时调用。

参数：  
* **上下文**：传递到 UnloadEngineAsync 操作的上下文。


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure 函数
在卸载引擎引发错误时调用。

参数：  
* error****：导致卸载引擎操作失败的错误。 


* **上下文**：传递到 UnloadEngineAsync 操作的上下文。


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。

参数：  
* **engine**：新添加的引擎 


* **上下文**：传递到 AddEngineAsync 操作的上下文


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting 函数
在创建引擎之前调用，用于描述是否必须从服务器中提取引擎的策略数据，或者是否可以从本地缓存的数据中创建它。

参数：  
* **requiresPolicyFetch**：描述是否必须通过 HTTP 获取引擎数据或是否从缓存中加载引擎数据


此可选回调可由应用程序使用，通知 AddEngineAsync 操作是否需要执行 HTTP 操作（及其关联的延迟）才能完成。
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎引发错误时调用。

参数：  
* error****：导致添加引擎操作失败的错误。 


* **上下文**：传递到 AddEngineAsync 操作的上下文。


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。

参数：  
* **上下文**：传递到 DeleteEngineAsync 操作的上下文。


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎引发错误时调用。

参数：  
* error****：导致删除引擎操作失败的错误。 


* **上下文**：传递到 DeleteEngineAsync 操作的上下文。


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged 函数
当具有给定 ID 的引擎的策略发生更改时，或在已加载的自定义敏感性类型发生更改时调用。

参数：  
* **engineId**：引擎 


若要加载新策略，需要再次使用指定引擎 ID 调用 AddEngineAsync。
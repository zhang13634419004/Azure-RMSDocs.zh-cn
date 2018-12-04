---
title: class mip PolicyEngine Settings
description: class mip PolicyEngine Settings 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6ac94d1e34615a0248dac85f28c55154b127574f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446339"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
定义与 [PolicyEngine](class_mip_policyengine.md) 关联的设置。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  用于加载现有引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  用于新建引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。
 public const std::string& GetEngineId() const  |  获取引擎 ID。
 public void SetEngineId(const std::string& id)  |  设置引擎 ID。
 public const Identity& GetIdentity() const  |  获取标识对象。
 public void SetIdentity(const Identity& identity)  |  设置标识对象。
 public const std::string& GetClientData() const  |  获取设置中设置的客户端数据。
 public void SetClientData(const std::string& clientData)  |  设置客户端数据字符串。
 public const std::string& GetLocale() const  |  获取设置中设置的区域设置。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  设置自定义设置，用于功能访问控制和测试。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  获取用于功能访问控制和测试的自定义设置。
 public void SetSessionId(const std::string& sessionId)  |  设置用于客户端定义遥测的会话 ID。
 public const std::string& GetSessionId() const  |  获取唯一标识符形式的会话 ID。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
用于加载现有引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。

参数：  
* **engineId**：将它设置为 AddEngineAsync 生成或自生成的唯一引擎 ID。 重新加载现有引擎时，将重用此 ID，否则将创建一个新引擎。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。


  
### <a name="settings"></a>设置
用于新建引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。

参数：  
* **identity**：与新引擎关联的用户的标识信息。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。


  
### <a name="getengineid"></a>GetEngineId
获取引擎 ID。

  
**返回结果**：标识引擎的唯一字符串。
  
### <a name="setengineid"></a>SetEngineId
设置引擎 ID。

参数：  
* **ID**：引擎 ID。


  
### <a name="getidentity"></a>GetIdentity
获取标识对象。

  
**返回结果**：对设置对象中的标识的引用。 
  
另请参阅：mip::Identity
  
### <a name="setidentity"></a>SetIdentity
设置标识对象。

参数：  
* **identity**：用户的唯一标识。 


  
另请参阅：mip::Identity
  
### <a name="getclientdata"></a>GetClientData
获取设置中设置的客户端数据。

  
**返回结果**：客户端指定的数据的字符串。
  
### <a name="setclientdata"></a>SetClientData
设置客户端数据字符串。

参数：  
* **clientData**：用户指定的数据。


  
### <a name="getlocale"></a>GetLocale
获取设置中设置的区域设置。

  
**返回结果**：区域设置。
  
### <a name="setcustomsettings"></a>SetCustomSettings
设置自定义设置，用于功能访问控制和测试。

参数：  
* **customSettings**：名称/值对列表。


  
### <a name="getcustomsettings"></a>GetCustomSettings
获取用于功能访问控制和测试的自定义设置。

  
**返回结果**：名称/值对列表。
  
### <a name="setsessionid"></a>SetSessionId
设置用于客户端定义遥测的会话 ID。

参数：  
* **sessionId**：连接遥测事件的唯一字符串。


  
### <a name="getsessionid"></a>GetSessionId
获取唯一标识符形式的会话 ID。

  
**返回结果**：会话 ID。
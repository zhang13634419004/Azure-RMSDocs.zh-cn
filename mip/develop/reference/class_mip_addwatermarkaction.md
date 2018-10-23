---
title: class mip AddWatermarkAction
description: class mip AddWatermarkAction 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f49bd7aa16ae12aef240d05fff6acf507ddc341d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446084"
---
# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
指定添加水印的操作类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  用于标记水印元素的 API。
 public WatermarkLayout GetLayout() const  |  用于获取水印布局的 API。
 public const std::string& GetText() const  |  获取应添加到水印的文本。
 public const std::string& GetFontName() const  |  获取用于显示水印的字体名称。
 public int GetFontSize() const  |  获取用于显示水印的字号。
 public const std::string& GetFontColor() const  |  获取用于显示水印的字体颜色。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getuielementname"></a>GetUIElementName
用于标记水印元素的 API。

  
**返回结果**：应用于保存水印的 UI 元素的名称。 如果需要删除水印，将在 RemoveWatermarkingAction 中返回相同名称。
  
### <a name="getlayout"></a>GetLayout
用于获取水印布局的 API。

  
**返回结果**：WatermarkLayout：采用枚举水平|对角线形式的水印布局。 、
  
### <a name="gettext"></a>GetText
获取应添加到水印的文本。

  
**返回结果**：内容头文本。
  
### <a name="getfontname"></a>GetFontName
获取用于显示水印的字体名称。

  
**返回结果**：字体名称。 如果策略未进行任何设置，默认值为 Calibri。
  
### <a name="getfontsize"></a>GetFontSize
获取用于显示水印的字号。

  
**返回结果**：整数形式的字体大小。
  
### <a name="getfontcolor"></a>GetFontColor
获取用于显示水印的字体颜色。

  
返回结果：字符串形式的字体颜色（例如“#000000”）。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。
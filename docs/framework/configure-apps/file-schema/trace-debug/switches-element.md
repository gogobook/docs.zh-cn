---
title: '&lt;交换机&gt;元素'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/switches
- http://schemas.microsoft.com/.NetConfiguration/v2.0#switches
helpviewer_keywords:
- <switches> element
- switches element
- trace switches, <switches> element
ms.assetid: 4cf36786-b89a-40e2-a0f1-86bb9b783343
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: 60a18ae8d89d6be69b2c10c07064f123d3f9c0f8
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32745141"
---
# <a name="ltswitchesgt-element"></a>&lt;交换机&gt;元素
包含跟踪开关和对该跟踪开关设置的级别。  
  
 \<configuration>  
\<system.diagnostics >  
\<交换机 >  
  
## <a name="syntax"></a>语法  
  
```xml  
      <switches>   
</switches>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-switches.md)|指定对跟踪开关设置的级别。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`System.diagnostics`|指定用于收集、存储和路由消息的跟踪侦听器以及对跟踪开关设置的级别。|  
  
## <a name="remarks"></a>备注  
 可以通过将它放在配置文件来更改跟踪开关的级别。 如果开关已<xref:System.Diagnostics.BooleanSwitch>，你可以将其打开和关闭。 如果开关已<xref:System.Diagnostics.TraceSwitch>，可以将不同级别分配到它，以指定类型的跟踪或调试消息的应用程序输出。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用**\<切换 >** 元素中设置`General`跟踪切换到<xref:System.Diagnostics.TraceLevel>级别，并启用`Data`布尔型跟踪开关。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
         <add name="Data" value="1" />  
      </switches>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Diagnostics.Switch>  
 <xref:System.Diagnostics.TraceSwitch>  
 <xref:System.Diagnostics.BooleanSwitch>  
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)

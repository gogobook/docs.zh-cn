---
title: "执行不区分区域性的字符串比较 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "区域性参数"
  - "不区分区域性的字符串操作, 比较"
  - "字符串比较 [.NET Framework], 不区分区域性"
  - "String.Compare 方法"
  - "String.CompareTo 方法"
  - "字符串 [.NET Framework], 比较"
ms.assetid: abae50ef-32f7-4a50-a540-fd256fd1aed0
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# 执行不区分区域性的字符串比较
默认情况下，<xref:System.String.Compare%2A?displayProperty=fullName> 方法执行区分区域性和区分大小写的比较。  此方法还包括多个重载，这些重载提供了一个 `culture` 参数和一个 `comparisonType` 参数，前者允许你指定要使用的区域性，后者允许你指定要使用的比较规则。  调用这些方法（而非调用默认重载）将消除与特定方法调用中使用的规则相关的任何歧义，并阐明某个特定比较是区分区域性的还是不区分区域性的。  
  
> [!NOTE]
>  <xref:System.String.CompareTo%2A?displayProperty=fullName> 方法的两种重载都执行区分区域性且区分大小写的比较；你不能使用此方法来执行不区分区域性的比较。  为了使代码简单明了，建议你改用 <xref:System.String.Compare%2A?displayProperty=fullName> 方法。  
  
 对于区分区域性的操作，请将 <xref:System.StringComparison?displayProperty=fullName> 或 <xref:System.StringComparison?displayProperty=fullName> 枚举值指定为 `comparisonType` 参数。  如果你希望使用当前区域性之外的某个指定区域性来执行区分区域性的比较时，请将表示该区域性的 <xref:System.Globalization.CultureInfo> 对象指定为 `culture`  参数。  
  
 <xref:System.String.Compare%2A?displayProperty=fullName> 方法所支持的不区分区域性的字符串比较可以是语义的（基于固定区域性的排序约定）或非语义的（基于字符串中字符的序号值）。  大多数不区分区域性的字符串比较是非语义的。  对于这些比较，请将 <xref:System.StringComparison?displayProperty=fullName> 或 <xref:System.StringComparison?displayProperty=fullName> 枚举值指定为 `comparisonType` 参数。  例如，如果安全决策（例如，用户名或密码比较）基于字符串比较的结果，则操作应不区分区域性且是非语义的，以确保结果不受特定区域性或语言的约定的影响。  
  
 如果你希望以一致方式处理来自多个区域性的语义相关字符串，请使用不区分区域性的语义字符串比较。  例如，如果你的应用程序在列表框中显示使用多个字符集的字词，则不管当前区域性如何，你可能都需要按相同的顺序来显示这些字词。  对于不区分区域性的语义比较，.NET Framework 将定义一个基于英语的语义约定的固定区域性。  若要执行不区分区域性的语义比较，请将 <xref:System.StringComparison?displayProperty=fullName> 或 <xref:System.StringComparison?displayProperty=fullName> 指定为 `comparisonType` 参数。  
  
 下面的示例将执行两个不区分区域性的非语义字符串比较。  第一个比较区分大小写，而第二个比较不区分大小写。  
  
 [!code-csharp[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/cs/cultureinsensitive1.cs#1)]
 [!code-vb[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/vb/cultureinsensitive1.vb#1)]  
  
## 请参阅  
 <xref:System.String.Compare%2A?displayProperty=fullName>   
 <xref:System.String.CompareTo%2A?displayProperty=fullName>   
 [执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)   
 [针对使用字符串的最佳做法](../../../docs/standard/base-types/best-practices-strings.md)
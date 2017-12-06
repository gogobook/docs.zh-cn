---
title: "快速入门 - 集合 - C# 指南"
description: "在本快速入门课程中通过探索列表集合了解 C#。"
keywords: "C#, 入门, 教程, 集合, 列表"
author: billwagner
ms.author: wiwagn
ms.date: 10/13/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 228a9dd88d0a511492ccb8b70e0231278969acbe
ms.sourcegitcommit: 43c656811dd38a66a6672084c65d10c0cbbf2015
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2017
---
# <a name="c-quick-start-collections"></a>C# 快速入门：集合 #

本快速入门介绍 C# 语言和的基础知识<xref:System.Collections.Generic.List%601>类。

本快速入门希望有一台计算机可用于开发。 .NET 主题[开始在 10 分钟后](https://www.microsoft.com/net/core)已设置你在 Mac、 PC 或 Linux 上的本地开发环境的说明。

## <a name="a-basic-list-example"></a>一个基本的列表的示例。

创建名为 list-quickstart 的目录。 将新建的目录设为当前目录，并运行 `dotnet new console`。

> [!NOTE]
> 如果你刚刚完成[在 10 分钟内开始使用.NET](https://www.microsoft.com/net)，你可以继续使用你刚刚创建的 myApp 应用程序。
 
在常用编辑器中，打开 Program.cs，并将现有代码替换为以下代码：

```csharp
using System;
using System.Collections.Generic;

namespace list_quickstart
{
    class Program
    {
        static void Main(string[] args)
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

将 `<name>` 替换为自己的名称。 保存 Program.cs。 在控制台窗口中键入 `dotnet run`，试运行看看。

刚刚创建了一个字符串列表，并向其中添加了三个名称，再输出了全部大写的名称。 循环读取整个列表需要用到在前面的快速入门课程中学到的概念。

用于显示名称的代码使用内插字符串。  如果 `$` 字符前面有 `string`，可以在字符串声明中嵌入 C# 代码。 实际字符串使用自己生成的值替换相应 C# 代码。 在此示例中，`{name.ToUpper()}` 被替换为各个转换为大写字母的名称，因为调用了 <xref:System.String.ToUpper%2A> 方法。

接下来将进一步探索。
    
## <a name="modify-list-contents"></a>修改列表内容

创建的集合使用 <xref:System.Collections.Generic.List%601> 类型。 此类型存储一系列元素。 元素类型是在尖括号内指定。
    
<xref:System.Collections.Generic.List%601> 类型的一个重要方面是，既可以扩大，也可以收缩，方便用户添加或删除元素。 在 `Main` 方法的右 `}` 前添加以下代码：

```csharp
Console.WriteLine();
names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

又向列表的末尾添加了两个名称。 同时，也删除了一个名称。 保存此文件，并键入 `dotnet run`，试运行看看。
    
借助 <xref:System.Collections.Generic.List%601>，还可以按索引引用各项。 索引位于列表名称后面的 `[` 和 `]` 令牌之间。 C# 对第一个索引使用 0。 将以下代码添加到刚才添加的代码的正下方，并试运行看看：

```csharp
Console.WriteLine($"My name is {names[0]}");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");
```

不得访问超出列表末尾的索引。 请注意，索引是从 0 开始编制，因此最大有效索引是用列表项数减 1 计算得出。 可以使用 <xref:System.Collections.Generic.List%601.Count%2A> 属性确定列表长度。 在 Main 方法的末尾，添加以下代码：

```csharp
Console.WriteLine($"The list has {names.Count} people in it");
 ```

保存此文件，并再次键入 `dotnet run` 看看结果如何。    

## <a name="search-and-sort-lists"></a>搜索列表并进行排序
我们的示例使用的列表较小，但大家的应用程序创建的列表通常可能会包含更多元素，有时可能会包含数以千计的元素。 若要在更大的集合中查找元素，需要在列表中搜索不同的项。 <xref:System.Collections.Generic.List%601.IndexOf%2A> 方法可搜索项，并返回此项的索引。 将以下代码添加到 `Main` 方法的底部：

```csharp
var index = names.IndexOf("Felipe");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
} else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");
}

index = names.IndexOf("Not Found");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
} else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");
    
}
```

还可以对列表中的项进行排序。 <xref:System.Collections.Generic.List%601.Sort%2A> 方法按正常顺序（按字母顺序，如果是字符串的话）对列表中的所有项进行排序。 将以下代码添加到 `Main` 方法的底部：

```csharp
names.Sort();
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

保存此文件，并键入 `dotnet run`，试运行此最新版程序。

开始进入下一部分前，先将当前代码移到单独的方法中。 这样一来，可以更轻松地开始处理新示例。 将 `Main` 方法重命名为 `WorkingWithStrings`，并编写调用 `WorkingWithStrings` 的新 `Main` 方法。 完成后，代码应如下所示：

```csharp
using System;
using System.Collections.Generic;

namespace list_quickstart
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkingWithStrings();
        }

        public static void WorkingWithStrings()
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine();
            names.Add("Maria");
            names.Add("Bill");
            names.Remove("Ana");
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine($"My name is {names[0]}");
            Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");

            Console.WriteLine($"The list has {names.Count} people in it");

            var index = names.IndexOf("Felipe");
            Console.WriteLine($"The name {names[index]} is at index {index}");

            var notFound = names.IndexOf("Not Found");
            Console.WriteLine($"When an item is not found, IndexOf returns {notFound}");

            names.Sort();
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

## <a name="lists-of-other-types"></a>其他类型的列表

到目前为止，大家一直在列表中使用 `string` 类型。 接下来，将让 <xref:System.Collections.Generic.List%601> 使用其他类型。 那就生成一组数字吧。 

将以下代码添加到新 `Main` 方法的底部：

```csharp
var fibonacciNumbers = new List<int> {1, 1};
```

这会创建一个整数列表，并将头两个整数设置为值 1。 这些是斐波那契数列（一系列数字）的头两个值。 斐波那契数列中的每个数字都是前两个数字之和。 添加以下代码：

```csharp
var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

fibonacciNumbers.Add(previous + previous2);

foreach(var item in fibonacciNumbers)
    Console.WriteLine(item);
```

保存此文件，并键入 `dotnet run` 看看结果如何。 

> [!TIP]
> 为了能够集中精力探究此部分，可以注释掉调用 `WorkingWithStrings();` 的代码。 只需在此调用前添加两个 `/` 字符即可，如 `// WorkingWithStrings();`。 

## <a name="challenge"></a>挑战
看看能不能将本课程中的一些内容与前面的课程融会贯通。 使用斐波那契数列，扩展当前生成的程序。 试着编写代码，生成此序列中的前 20 个数字。

## <a name="complete-challenge"></a>完成挑战

可以[查看 GitHub 上的完成示例代码](https://github.com/dotnet/docs/tree/master/samples/csharp/list-quickstart/Program.cs#L13-L23)，了解示例解决方案

在循环的每次迭代中，取此列表中的最后两个整数进行求和，并将计算出的总和值添加到列表中。 循环会一直重复运行到列表中有 20 个项为止。

祝贺你，你已完成列表快速入门。 您可以使用继续[简介类](introduction-to-classes.md)开发环境中的快速入门。

若要详细了解如何使用 `List` 类型，可以参阅有关[集合](../../standard/collections/index.md)的 [.NET 指南](../../standard/index.md)主题。 还可以了解其他许多集合类型。
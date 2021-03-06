---
title: 如何：使用 BindingSource 和 INotifyPropertyChanged 接口引发更改通知
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- change notifications [Windows Forms], raising
- BindingSource component [Windows Forms], and IPropertyChange
- data sources [Windows Forms], detecting changes
- examples [Windows Forms], BindingSource component
- change notifications
- INotifyPropertyChanged interface [Windows Forms], using with BindingSource
- BindingSource component [Windows Forms], examples
ms.assetid: 7fa2cf51-c09f-4375-adf0-e36c5617f099
ms.openlocfilehash: 44efe12fb6494766f9c6cd7a18bd030c9b92f4bd
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33538286"
---
# <a name="how-to-raise-change-notifications-using-a-bindingsource-and-the-inotifypropertychanged-interface"></a>如何：使用 BindingSource 和 INotifyPropertyChanged 接口引发更改通知
<xref:System.Windows.Forms.BindingSource> 组件将在数据源中包含的类型实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口时自动删除数据源中的更改，并在属性值更改时引发 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 事件。 上述操作非常有用，因为已绑定到 <xref:System.Windows.Forms.BindingSource> 的控件之后会在数据源值更改时自动更新。  
  
> [!NOTE]
>  如果数据源实现 <xref:System.ComponentModel.INotifyPropertyChanged>，并且你正在执行异步操作，则不应更改后台线程上的数据源。 相反，应读取后台线程上的数据，并将数据合并到 UI 线程上的列表。  
  
## <a name="example"></a>示例  
 下面的代码示例演示了如何简单实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口。 它还演示了当将 <xref:System.Windows.Forms.BindingSource> 绑定到 <xref:System.ComponentModel.INotifyPropertyChanged> 类型的列表时，<xref:System.Windows.Forms.BindingSource> 如何将数据源更改自动传递到绑定控件。  
  
 如果使用 `CallerMemberName` 特性，则调用 `NotifyPropertyChanged` 方法不必将属性名称指定为字符串参数。 有关详细信息，请参阅[调用方信息](http://msdn.microsoft.com/library/9cb2b8c0-c4f6-44b8-9c90-38948455b373)。  
  
 [!code-csharp[System.ComponentModel.IPropertyChangeExample#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.IPropertyChangeExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System、System.Data、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 为 Visual Basic 或 Visual C# 中生成此示例从命令行有关的信息，请参阅[从命令行生成](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe 生成](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 你也可以通过将代码粘贴到新项目中生成 Visual Studio 中的此示例。  另请参阅[超链接"http://msdn.microsoft.com/library/Bb129228(v=vs.110)"如何： 编译和运行完整 Windows 窗体代码示例使用 Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.ComponentModel.INotifyPropertyChanged>  
 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)  
 [如何：使用 BindingSource ResetItem 方法引发更改通知](../../../../docs/framework/winforms/controls/how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)

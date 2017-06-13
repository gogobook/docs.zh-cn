---
title: "使用二进制数据（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 二进制数据"
  - "WCF 数据服务, 流"
ms.assetid: aeccc45c-d5c5-4671-ad63-a492ac8043ac
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 使用二进制数据（WCF 数据服务）
利用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库，您可以通过以下方式之一从 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源中检索二进制数据并进行更新。  
  
-   作为实体的基元类型属性。  当使用可轻松加载到内存中的小型二进制数据对象时，建议使用此方法。  在这种情况下，二进制属性是数据模型公开的实体属性，而数据服务会在响应消息中将二进制数据序列化为 base\-64 二进制编码的 XML。  
  
-   作为单独的二进制资源流。  当访问和更改可能表示照片、视频或其他任何类型的二进制编码数据的二进制大型对象 \(BLOB\) 数据时，建议使用此方法。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]通过使用 HTTP 实现二进制数据流，如 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 中定义。  在此机制中，二进制数据被视为独立于实体但又与实体相关的媒体资源，这称为媒体链接入口。  有关详细信息，请参阅[流提供程序](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md)。  
  
> [!TIP]
>  有关如何创建一个 [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] 客户端应用程序（它从存储照片的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务下载二进制图像文件）的逐步示例，请参见[数据服务流提供程序系列文章 \- 第 2 部分：从客户端访问媒体资源流](http://go.microsoft.com/fwlink/?LinkId=201637)（可能为英文网页）一文。  要下载博客文章中的流照片数据服务的示例代码，请参见 MSDN 代码库中的[流照片数据服务示例](http://go.microsoft.com/fwlink/?LinkId=198988)（可能为英文网页）。  
  
## 实体元数据  
 具有相关媒体资源流的实体由应用于实体类型（媒体链接入口）的 `HasStream` 属性在数据服务元数据中表示。  在下面的示例中，`PhotoInfo` 实体是媒体链接入口，它具有一个由 `HasStream` 属性表示的相关媒体资源。  
  
 [!code-xml[Astoria Photo Streaming Service#HasStream](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria photo streaming service/xml/photodata.edmx#hasstream)]  
  
 本主题中的其余示例揭示了如何访问和更改媒体资源流。  有关如何通过使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库在 .NET Framework 客户端应用程序中使用媒体资源的完整示例，请参见[从客户端访问媒体资源流](http://go.microsoft.com/fwlink/?LinkID=201637)（可能为英文网页）一文。  
  
## 访问二进制资源流  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库提供了从基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的数据服务访问二进制资源流的方法。  下载媒体资源时，可以使用媒体资源的 URI，也可以获取一个包含媒体资源数据本身的二进制流。  还可以上载媒体资源数据作为一个二进制流。  
  
> [!TIP]
>  有关如何创建一个 [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] 客户端应用程序（它从存储照片的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务下载二进制图像文件）的逐步示例，请参见[数据服务流提供程序系列文章 \- 第 2 部分：从客户端访问媒体资源流](http://go.microsoft.com/fwlink/?LinkId=201637)（可能为英文网页）一文。  要下载博客文章中的流照片数据服务的示例代码，请参见 MSDN 代码库中的[流照片数据服务示例](http://go.microsoft.com/fwlink/?LinkId=198988)（可能为英文网页）。  
  
### 获取二进制流的 URI  
 检索某些类型的媒体资源（如图像和其他媒体文件）时，在应用程序中使用媒体资源的 URI 通常比处理二进制数据流本身更容易。  要获取与给定媒体链接入口相关联的资源流的 URI，必须对跟踪实体的 <xref:System.Data.Services.Client.DataServiceContext> 实例调用 <xref:System.Data.Services.Client.DataServiceContext.GetReadStreamUri%2A> 方法。  下面的示例揭示了如何调用 <xref:System.Data.Services.Client.DataServiceContext.GetReadStreamUri%2A> 方法以获取用于在客户端上创建新图像的媒体资源流的 URI：  
  
 [!code-csharp[Astoria Photo Streaming Client#GetReadStreamUri](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria photo streaming client/cs/photowindow.xaml.cs#getreadstreamuri)]
 [!code-vb[Astoria Photo Streaming Client#GetReadStreamUri](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria photo streaming client/vb/photowindow.xaml.vb#getreadstreamuri)]  
  
### 下载二进制资源流  
 检索二进制资源流时，必须对跟踪媒体链接入口的 <xref:System.Data.Services.Client.DataServiceContext> 实例调用 <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> 方法。  该方法向数据服务发送一个返回 <xref:System.Data.Services.Client.DataServiceStreamResponse> 对象的请求，该对象具有对包含资源的流的引用。  当应用程序要求将二进制资源作为 <xref:System.IO.Stream> 时可使用该方法。  下面的示例揭示了如何调用 <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> 方法以检索用于在客户端上创建新图像的流：  
  
 [!code-csharp[Astoria Streaming Client#GetReadStreamClient](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria streaming client/cs/customerphotowindow.xaml.cs#getreadstreamclient)]
 [!code-vb[Astoria Streaming Client#GetReadStreamClient](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria streaming client/vb/customerphotowindow.xaml.vb#getreadstreamclient)]  
  
> [!NOTE]
>  数据服务不会设置包含二进制数据流的响应消息中的 Content\-Length 标头。  此值可能不反映二进制数据流的实际长度。  
  
### 将媒体资源作为流上载  
 若要插入或更新媒体资源，请对正在跟踪实体的 <xref:System.Data.Services.Client.DataServiceContext> 实例调用 <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> 方法。  此方法向包含从所提供的流中读取的媒体资源的数据服务发送请求。  下面的示例揭示了如何调用 <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> 方法以向数据服务发送图像：  
  
 [!code-csharp[Astoria Photo Streaming Client#SetSaveStream](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria photo streaming client/cs/photodetailswindow.xaml.cs#setsavestream)]
 [!code-vb[Astoria Photo Streaming Client#SetSaveStream](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria photo streaming client/vb/photodetailswindow.xaml.vb#setsavestream)]  
  
 在此示例中，通过为 `closeStream` 参数提供 `true` 值，调用 <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> 方法。  这样可保证在将二进制数据上载到数据服务之后，<xref:System.Data.Services.Client.DataServiceContext> 将会关闭流。  
  
> [!NOTE]
>  调用 <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> 时，只有在调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 之后，才会将流发送到数据服务。  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [将数据绑定到控件](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)
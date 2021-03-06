---
title: "&lt;dateTimeSerialization&gt; 要素"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- dateTimeSerialization element
- XML serialization, configuration
- <dateTimeSerialization> element
ms.assetid: 90fda55c-7730-41e9-bc4b-6423a4b920af
caps.latest.revision: 5
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 9ced207c17355cc9c1bd85bdada4208dea2ceb2f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="ltdatetimeserializationgt-element"></a>&lt;dateTimeSerialization&gt; 要素
<xref:System.DateTime> オブジェクトのシリアル化モードを決定します。  
  
 \<configuration>  
\<dateTimeSerialization>  
  
## <a name="syntax"></a>構文  
  
```xml  
<dateTimeSerialization  
    mode = "Roundtrip" | "Local"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|----------------|-----------------|  
|`mode`|省略可能です。 シリアル化モードを指定します。 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode> 値のいずれかに設定します。 既定値は **RoundTrip** です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|system.xml.serialization|XML シリアル化を制御する最上位の要素です。|  
  
## <a name="remarks"></a>コメント  
 .NET Framework の 1.0、1.1、2.0、およびそれ以降のバージョンで、このプロパティが **Local** に設定されている場合、<xref:System.DateTime> オブジェクトは常に現地時刻として書式設定されます。 つまり、ローカル タイム ゾーンの情報が、シリアル化されたデータに必ず組み込まれます。 .NET Framework の以前のバージョンとの互換性を保証するには、このプロパティを **Local** に設定します。  
  
 このプロパティが **Roundtrip** に設定されているバージョン 2.0 以降の .NET Framework では、<xref:System.DateTime> オブジェクトが調べられ、タイム ゾーンがローカル、UTC、または未指定のいずれであるかが特定されます。 その後、この特定された情報を保持する形で、<xref:System.DateTime> オブジェクトがシリアル化されます。 これは既定の動作であり、.NET Framework の以前のバージョンと通信を行わない、すべての新しいアプリケーションで推奨されます。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.DateTime>   
 <xref:System.Xml.Serialization.XmlSchemaImporter>   
 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>   
 [構成ファイル スキーマ](../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<schemaImporterExtensions> 要素](../../../docs/standard/serialization/schemaimporterextensions-element.md)   
 [\<xmlSchemaImporterExtensions> の \<add> 要素](../../../docs/standard/serialization/add-element-for-xmlschemaimporterextensions.md)   
 [\<system.xml.serialization> 要素](../../../docs/standard/serialization/system-xml-serialization-element.md)


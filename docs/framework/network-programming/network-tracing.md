---
title: ".NET Framework のネットワークのトレース"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
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
- debugging [.NET Framework], network tracing
- methods, network tracing
- Networking
- trace enabled debugging
- network tracing, about network tracing
- network tracing
- network, network tracing
- traffic tracing
- tracing [.NET Framework], network
- deploying applications [.NET Framework], network traffic
- capturing network traffic
- Internet, network tracing
- Network Resources
- output, network tracing
- method invocations
ms.assetid: e993b7c3-087f-45d8-9c02-9dded936d804
caps.latest.revision: 9
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c8c915edee4fe23b1718f4820eff9998fa9e5836
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="network-tracing-in-the-net-framework"></a>.NET Framework のネットワークのトレース
.NET Framework のネットワークのトレースでは、メソッド呼び出しについての情報、およびマネージ アプリケーションによって生成されるネットワーク トラフィックについての情報にアクセスできます。 この機能は、開発中のアプリケーションのデバッグや、配置済みのアプリケーションの分析に役立ちます。 ネットワークのトレースの出力は、開発時および稼動環境でのさまざまな使用方法をサポートするようにカスタマイズできます。  
  
 .NET Framework でのネットワークのトレースを有効にするには、トレースの出力先を選択し、アプリケーションまたはコンピューターの構成ファイルにネットワークのトレースの構成設定を追加する必要があります。 構成ファイルの内容、およびそれらの使用方法については、「[構成ファイル](../../../docs/framework/configure-apps/index.md)」を参照してください。 ネットワークのトレースを有効にする方法については、「[ネットワークのトレースを有効にする](../../../docs/framework/network-programming/enabling-network-tracing.md)」を参照してください。 構成ファイルに追加する必要がある設定については、「[方法: ネットワークのトレースを構成する](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)」を参照してください。  
  
 トレースが有効なときは、**System.Net** クラスによって出力されるトレース情報をキャプチャできます。 トレース情報を生成するネットワーク クラスのメンバーについては、.NET Framework クラス ライブラリのドキュメントの「解説」セクションに次のメモが含まれます。  
  
> [!NOTE]
>  このメンバーは、アプリケーションでネットワーク トレースが有効にされている場合にトレース情報を出力します。 詳細については、「ネットワークのトレース」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ネットワークのトレースの有効化](../../../docs/framework/network-programming/enabling-network-tracing.md)   
 [方法: ネットワークのトレースを構成する](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)   
 [ネットワークのトレースの解釈](../../../docs/framework/network-programming/interpreting-network-tracing.md)   
 [実装とトレースの概要](http://msdn.microsoft.com/en-us/e924e57c-33cf-4b0e-9e7f-a45d13e38f2c)


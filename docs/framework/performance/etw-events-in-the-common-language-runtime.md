---
title: "共通言語ランタイムの ETW イベント"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CLR ETW events
- ETW, common language runtime
- ETW, CLR events
ms.assetid: 5bb9b6a2-7b57-4aea-8809-32b28bc73e88
caps.latest.revision: 7
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6a6b97bf8ce9075ee5fc8877fed65bd4a23f1ce5
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="etw-events-in-the-common-language-runtime"></a>共通言語ランタイムの ETW イベント
共通言語ランタイム (CLR) は、さまざまなデバッグとプロファイリング イベントを通じて、有用な Windows イベント トレーシング (ETW) の診断情報を提供します。 CLR ETW イベントは、Windows ETW トレース システムを利用して、共通言語ランタイムによって提供される既存のプロファイリングとデバッグのサポートを拡張します。  
  
 ETW の詳細については、MSDN で「[Improve Debugging and Performance Tuning with ETW](http://go.microsoft.com/fwlink/?LinkID=161142)」 (ETW によるデバッグとパフォーマンス チューニングの向上) の記事を参照してください。 Xperf に関する情報は、NTDebugging のブログ エントリ「[Windows Performance Toolkit - Xperf](http://go.microsoft.com/fwlink/?LinkID=161144)」にあります。  
  
 追加の CLR ETW ツールは、利用可能になると、[CodePlex Web サイト](http://go.microsoft.com/fwlink/?LinkID=111138)で提供されます。  
  
 イベント トピックに記載されているすべてのイベントには、[!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 以降が必要です。 Windows Vista オペレーティング システムは、サポートされる最小のクライアントで、Windows Server 2008 は、サポートされる最小のサーバーです。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [.NET Framework のログ記録の制御](../../../docs/framework/performance/controlling-logging.md)  
 ETW イベントをキャプチャおよび表示するためのツールとコマンドについて説明します。  
  
 [CLR ETW プロバイダー](../../../docs/framework/performance/clr-etw-providers.md)  
 ランタイム プロバイダーとランダウン プロバイダーの情報、およびこれらを使用して ETW データを収集する方法を提供します。  
  
 [CLR ETW キーワードおよびレベル](../../../docs/framework/performance/clr-etw-keywords-and-levels.md)  
 イベントをカテゴリ別にフィルタ処理できるランタイム プロバイダーとランダウン プロバイダーのキーワードについて説明します。  
  
 [CLR ETW イベント](../../../docs/framework/performance/clr-etw-events.md)  
 CLR ETW イベント、キーワード、レベル、およびイベント データに関する詳細情報を提供します。  
  
## <a name="see-also"></a>関連項目  
 [.NET Framework の ETW イベント](../../../docs/framework/performance/etw-events.md)


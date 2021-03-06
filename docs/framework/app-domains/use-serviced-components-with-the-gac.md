---
title: "サービス コンポーネントとグローバル アセンブリ キャッシュの使用"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache), serviced components
- serviced components, global assembly cache
- global assembly cache, serviced components
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 493ca9a2da4a06528eab9b87db78a5b7a49a2f1d
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="using-serviced-components-with-the-global-assembly-cache"></a>サービス コンポーネントとグローバル アセンブリ キャッシュの使用
サービス コンポーネント (マネージ COM+ コンポーネント) はグローバル アセンブリ キャッシュに配置する必要があります。 共通言語ランタイムと COM+ サービスは、シナリオによって、グローバル アセンブリ キャッシュに配置されていないサービス コンポーネントを処理できる場合と、処理できない場合があります。 これについて、次のシナリオで説明します。  
  
-   COM+ サーバー アプリケーションに含まれるサービス コンポーネントの場合、コンポーネントが含まれるアセンブリがグローバル アセンブリ キャッシュに配置されている必要があります。これは、Dllhost.exe がサービス コンポーネントを格納するのと同じディレクトリで実行されないためです。  
  
-   COM+ ライブラリ アプリケーションに含まれるサービス コンポーネントの場合、ランタイムと COM+ サービスは、現在のディレクトリで検索することにより、コンポーネントを含むアセンブリへの参照を解決できます。 この場合、アセンブリがグローバル アセンブリ キャッシュ内に配置されている必要はありません。  
  
-   ASP.NET アプリケーションに含まれるサービス コンポーネントの場合、状況は異なります。 サービス コンポーネントを含むアセンブリをアプリケーション ベースの bin ディレクトリに配置し、オンデマンド登録を使用すると、アセンブリはダウンロード キャッシュにシャドウとしてコピーされます。これは、ASP.NET がランタイムのシャドウ機能を利用するためです。  
  
## <a name="see-also"></a>関連項目  
 [アセンブリとグローバル アセンブリ キャッシュの使用](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Gacutil.exe (グローバル アセンブリ キャッシュ ツール)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)


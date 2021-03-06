---
title: gcUnmanagedToManaged MDA
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- GC unmanaged to managed
- transitioning threads unmanaged to managed code
- GcUnmanagedToManaged MDA
- threading [.NET Framework], garbage collection
- managed debugging assistants (MDAs), garbage collection
- threading [.NET Framework], managed debugging assistants
- garbage collection, run-time errors
- unmanaged to managed garbage collection
ms.assetid: 103eb3a3-1cf0-4406-8a9a-a7798fdc22d1
caps.latest.revision: 14
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1e484e3ec6af0d742263ec45a2a3081c221d9c61
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="gcunmanagedtomanaged-mda"></a>gcUnmanagedToManaged MDA
`gcUnmanagedToManaged` マネージ デバッグ アシスタント (MDA: Managed Debugging Assistant) は、スレッドがアンマネージ コードからマネージ コードに遷移する時に、毎回ガベージ コレクションが行われるようにします。  
  
## <a name="symptoms"></a>症状  
 COM およびプラットフォーム呼び出しを使用してアンマネージ ユーザー コンポーネントを実行中のアプリケーションによって、CLR で非確定的なアクセス違反が発生します。  
  
## <a name="cause"></a>原因  
 アプリケーションがアンマネージ ユーザー コンポーネントを実行中の場合、それらのコンポーネントによって、ガベージ コレクトされたヒープが破損された可能性があります。 これが原因で、ガベージ コレクターがオブジェクト グラフをウォークしようとしたときに、CLR でアクセス違反が発生します。  
  
## <a name="resolution"></a>解決策  
 このアシスタントを有効にすると、各マネージ遷移の前にガベージ コレクションが必ず行われるようになるため、アンマネージ コンポーネントがガベージ コレクトされたヒープを破損してから、アクセス違反が発生するまでの時間が短縮されます。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 スレッドがアンマネージ コードからマネージ コードに遷移する時に、毎回ガベージ コレクションが行われるようになります。  
  
## <a name="output"></a>出力  
 この MDA は、出力を生成しません。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <gcUnmanagedToManaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [マネージ デバッグ アシスタントによるエラーの診断](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [gcManagedToUnmanaged](../../../docs/framework/debug-trace-profile/gcmanagedtounmanaged-mda.md)   
 [相互運用マーシャリング](../../../docs/framework/interop/interop-marshaling.md)


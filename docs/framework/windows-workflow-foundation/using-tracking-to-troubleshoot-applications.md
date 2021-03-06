---
title: "追跡を使用したアプリケーションのトラブルシューティング | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8851adde-c3c2-4391-9523-d8eb831490af
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 追跡を使用したアプリケーションのトラブルシューティング
[!INCLUDE[wf](../../../includes/wf-md.md)] を使用すると、ワークフロー関連の情報を追跡して、詳細を [!INCLUDE[wf2](../../../includes/wf2-md.md)] アプリケーションまたはサービスの実行に提供できます。[!INCLUDE[wf2](../../../includes/wf2-md.md)] ホストでは、ワークフロー インスタンスの実行中に、ワークフロー イベントをキャプチャできます。ワークフローがエラーまたは例外を生成すると、[!INCLUDE[wf2](../../../includes/wf2-md.md)] の追跡の詳細を使用して処理の問題を解決できます。  
  
## WF の追跡を使用した WF のトラブルシューティング  
 [!INCLUDE[wf2](../../../includes/wf2-md.md)] アクティビティの処理内のエラーを検出するために、Faulted の状態を持つ <xref:System.Activities.Tracking.ActivityStateRecord> を照会する追跡プロファイルを使用して追跡を有効にすることができます。対応するクエリは、次のコードで指定されています。  
  
```  
<activityStateQueries>  
              <activityStateQuery activityName="*">  
                <states>  
                  <state name="Faulted" />  
                </states>  
              </activityStateQuery>  
 </activityStateQueries>  
```  
  
 エラーがエラー ハンドラー \(<xref:System.Activities.Statements.TryCatch> アクティビティなど\) 内で反映および処理される場合、<xref:System.Activities.Tracking.FaultPropagationRecord> を使用して検出できます。<xref:System.Activities.Tracking.FaultPropagationRecord> は、エラーのソース アクティビティとエラー ハンドラーの名前を示します。<xref:System.Activities.Tracking.FaultPropagationRecord> には、エラーに関する例外スタックの形式でエラーの詳細が含まれます。<xref:System.Activities.Tracking.FaultPropagationRecord> を定期受信するクエリを次の例に示します。  
  
```  
<faultPropagationQueries>  
              <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>  
 </faultPropagationQueries>  
  
```  
  
 エラーがワークフロー内で処理されない場合は、ワークフロー インスタンスでハンドルされない例外になり、ワークフロー インスタンスは中止されます。ハンドルされない例外の詳細を把握するために、追跡プロファイルでは、次のように `state name=”UnhandledException”` を持つワークフロー インスタンス レコードを照会する必要があります。  
  
```  
<workflowInstanceQueries>  
              <workflowInstanceQuery>  
                <states>  
                  <state name="UnhandledException" />  
                </states>  
              </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
 [!INCLUDE[wf2](../../../includes/wf2-md.md)] の追跡が有効になっている場合、ワークフロー インスタンスでハンドルされていない例外が発生すると、<xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord> オブジェクトが出力されます。  
  
 この追跡レコードには、例外スタックの形式でエラーの詳細が含まれます。この詳細には、失敗し、ハンドルされない例外になったエラーのソース \(アクティビティなど\) の詳細が含まれます。[!INCLUDE[wf2](../../../includes/wf2-md.md)] のエラー イベントを定期受信するには、追跡参加要素を追加することによって、追跡を有効にします。この参加要素は、`ActivityStateQuery (state=”Faulted”)`、<xref:System.Activities.Tracking.FaultPropagationRecord>、および `WorkflowInstanceQuery (state=”UnhandledException”)` を照会する追跡プロファイルで構成します。  
  
 ETW 追跡参加要素を使用して追跡を有効にした場合、エラー イベントは ETW セッションに書き出されます。イベントはイベント ビューアーを使用して表示できます。これは、分析チャネルのノードで **\[イベント ビューアー\]**、**\[アプリケーションとサービス ログ\]**、**\[Microsoft\]**、**\[Windows\]** の順に選択して、**\[アプリケーション サーバー \- アプリケーション\]** で確認できます。  
  
## 参照  
 [Windows Server App Fabric の監視](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [App Fabric を使用したアプリケーションの監視](http://go.microsoft.com/fwlink/?LinkId=201275)
---
title: "Pick アクティビティ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3e49b7f-0285-4720-8c09-11ae18f0d53e
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Pick アクティビティ
<xref:System.Activities.Statements.Pick> アクティビティを使用すると、イベント トリガー セットとそれに続く対応するハンドラーのモデル化が単純になります。  <xref:System.Activities.Statements.Pick> アクティビティには、<xref:System.Activities.Statements.PickBranch> アクティビティのコレクションが含まれます。各 <xref:System.Activities.Statements.PickBranch> は、<xref:System.Activities.Statements.PickBranch.Trigger%2A> アクティビティと <xref:System.Activities.Statements.PickBranch.Action%2A> アクティビティの組み合わせです。  実行時に、すべての分岐のトリガーが並行して実行されます。  1 つのトリガーが完了すると、対応するアクションが実行され、その他すべてのトリガーが取り消されます。  [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]<xref:System.Activities.Statements.Pick> アクティビティの動作は、[!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]<xref:System.Workflow.Activities.Listen> アクティビティに似ています。  
  
 次の「[Pick アクティビティの使用](../../../docs/framework/windows-workflow-foundation/samples/using-the-pick-activity.md)」に含まれる SDK サンプルのスクリーンショットは、2 つの分岐がある Pick アクティビティを示しています。  1 つ目の分岐には **Read input** というトリガーがあります。これはコマンド ラインから入力を読み取るカスタム アクティビティです。 2 つ目の分岐には <xref:System.Activities.Statements.Delay> アクティビティ トリガーがあります。 <xref:System.Activities.Statements.Delay> アクティビティが完了する前に **Read input** アクティビティがデータを受信した場合、<xref:System.Activities.Statements.Delay> が取り消され、メッセージがコンソールに書き込まれます。  それ以外の場合、**Read input** が割り当て時間内にデータを受信しないときは、アクティビティは取り消され、タイムアウト メッセージがコンソールに書き込まれます。  これは、任意のアクションにタイムアウトを追加するために使用される一般的なパターンです。  
  
 ![Pick アクティビティ](../../../docs/framework/windows-workflow-foundation//media/pickconceptual.JPG "PickConceptual")  
  
## <a name="best-practices"></a>ベスト プラクティス  
 Pick を使用する場合、実行する分岐は、トリガーが最初に完了する分岐です。  概念的には、すべてのトリガーは並行して実行され、1 つのトリガーがロジックの大部分を実行してから、他のトリガーが完了したために実行が取り消されることがあります。  この点に留意すると、Pick アクティビティを使用する場合に従う一般的なガイドラインは、トリガーを単一のイベントの代表として扱い、できるだけ少ないロジックを含めることです。  理想的には、トリガーにはイベントを受信するために必要なロジックのみを含め、そのイベントのすべての処理を分岐のアクションに含めます。  この方法で、トリガーの実行の重複を最小限に抑えることができます。  たとえば、2 つのトリガーを含む <xref:System.Activities.Statements.Pick> があるとします。各トリガーには <xref:System.ServiceModel.Activities.Receive> アクティビティとそれに続いて追加のロジックが含まれます。  追加のロジックによってアイドル ポイントが発生する場合、両方の <xref:System.ServiceModel.Activities.Receive> は正常に完了する可能性があります。  1 つのトリガーが完全に完了し、もう 1 つのトリガーは部分的に完了します。  一部のシナリオでは、メッセージを受け入れてから、その処理を部分的に完了することは許容されません。  したがって、<xref:System.ServiceModel.Activities.Receive> や <xref:System.ServiceModel.Activities.SendReply> など、WF のビルトイン メッセージング アクティビティを使用する場合、一般的には <xref:System.ServiceModel.Activities.Receive> がトリガーに使用されますが、可能な限り <xref:System.ServiceModel.Activities.SendReply> や他のロジックをアクションに含める必要があります。  
  
## <a name="using-the-pick-activity-in-the-designer"></a>デザイナーでの Pick アクティビティの使用  
 デザイナーで Pick を使用するには、ツールボックスで **[Pick]** と **[PickBranch]** を見つけます。  **[Pick]** をキャンバスにドラッグ アンド ドロップします。  既定では、デザイナーに新しく追加された **Pick** アクティビティには 2 つの分岐があります。  新しい分岐を追加するには、**PickBranch** アクティビティを既存の分岐の横にドラッグ アンド ドロップします。 アクティビティは、任意の **PickBranch** の **[Trigger]** 領域または **[Action]** 領域の **Pick** アクティビティにドロップできます。  
  
## <a name="using-the-pick-activity-in-code"></a>コードでの Pick アクティビティの使用  
 <xref:System.Activities.Statements.Pick> アクティビティを使用するには、<xref:System.Activities.Statements.PickBranch> アクティビティで <xref:System.Activities.Statements.Pick.Branches%2A> コレクションを設定します。 各 <xref:System.Activities.Statements.PickBranch> アクティビティには、<xref:System.Activities.Activity> 型の <xref:System.Activities.Statements.PickBranch.Trigger%2A> プロパティがあります。 指定したアクティビティの実行が完了すると、<xref:System.Activities.Statements.PickBranch.Action%2A> が実行されます。  
  
 次のコードは、<xref:System.Activities.Statements.Pick> アクティビティを使用して、コンソールからの入力を読み取るアクティビティのタイムアウトを実装する方法の例です。  
  
```csharp  
Sequence body = new Sequence()  
{  
    Variables = { name },  
    Activities =   
   {  
       new System.Activities.Statements.Pick  
        {  
           Branches =   
           {  
               new PickBranch  
               {  
                   Trigger = new ReadLine  
                   {  
                      Result = name,  
                      BookmarkName = "name"  
                   },  
                   Action = new WriteLine   
                   {   
                       Text = ExpressionServices.Convert<string>(ctx => "Hello " +   
                           name.Get(ctx))   
                   }  
               },  
               new PickBranch  
               {  
                   Trigger = new Delay  
                   {  
                      Duration = new TimeSpan(0, 0, 5)  
                   },  
                   Action = new WriteLine  
                   {  
                      Text = "Time is up."  
                   }  
               }  
           }  
       }  
   }  
};  
  
```  
  
```xaml  
<Sequence xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <Variable x:TypeArguments="x:String" Name="username" />  
  </Sequence.Variables>  
  <Pick>  
    <PickBranch>  
      <PickBranch.Trigger>  
        <ReadLine BookmarkName="name" Result="username" />  
      </PickBranch.Trigger>  
      <WriteLine>[String.Concat("Hello ", username)]</WriteLine>  
    </PickBranch>  
    <PickBranch>  
      <PickBranch.Trigger>  
        <Delay>00:00:05</Delay>  
      </PickBranch.Trigger>  
      <WriteLine>Time is up.</WriteLine>  
    </PickBranch>  
  </Pick>  
</Sequence>  
  
```
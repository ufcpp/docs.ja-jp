---
title: "Cert2spc.exe (ソフトウェア発行元証明書テスト ツール)"
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
- SPC
- Software Publisher Certificate Test tool
- Software Publisher Certificate
- Cert2spc.exe
- certificates, Software Publisher's Certificate
ms.assetid: be434d7d-9c0d-46e7-8392-58a9b542d11d
caps.latest.revision: 21
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7109f96b6997670afa6ef7c362b9e1a142014fbe
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="cert2spcexe-software-publisher-certificate-test-tool"></a>Cert2spc.exe (ソフトウェア発行元証明書テスト ツール)
ソフトウェア発行元証明書テスト ツールは、1 つ以上の X.509 証明書からソフトウェア発行元証明書 (SPC: Software Publisher's Certificate) を作成します。 Cert2spc.exe はテスト専用のツールです。 有効な SPC は、VeriSign や Thawte などの証明書発行機関から入手できます。 X.509 証明書の作成の詳細については、「[Makecert.exe (証明書作成ツール)](http://msdn.microsoft.com/library/b0343f8e-9c41-4852-a85c-f8a0c408cf0d)」を参照してください。  
  
 このツールは、Visual Studio と共に自動的にインストールされます。 このツールを実行するには、開発者コマンド プロンプト (または、Windows 7 の Visual Studio コマンド プロンプト) を使用します。 詳細については、「[コマンド プロンプト](../../../docs/framework/tools/developer-command-prompt-for-vs.md)」を参照してください。  
  
 コマンド プロンプトに次のように入力します。  
  
## <a name="syntax"></a>構文  
  
```  
cert2spc cert1.cer | crl1.crl [... certN.cer | crlN.crl] outputSPCfile.spc  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|引数|説明|  
|--------------|-----------------|  
|`certN.cer`|SPC ファイルに組み込む X.509 証明書の名前。 スペースで区切ることによって、複数の名前を指定できます。|  
|`crlN.crl`|SPC ファイルに組み込む証明書失効リストの名前。 スペースで区切ることによって、複数の名前を指定できます。|  
|`outputSPCfile.spc`|X.509 証明書が格納される PKCS #7 オブジェクトの名前。|  
  
|オプション|説明|  
|------------|-----------------|  
|**/?**|このツールのコマンド構文とオプションを表示します。|  
  
## <a name="examples"></a>例  
 `myCertificate.cer` から SPC を作成し、`mySPCFile.spc` に格納するコマンドを次に示します。  
  
```  
cert2spc myCertificate.cer mySPCFile.spc  
```  
  
 `oneCertificate.cer` と `twoCertificate.cer` から SPC を作成し、`mySPCFile.spc` に格納するコマンドを次に示します。  
  
```  
cert2spc oneCertificate.cer twoCertificate.cer mySPCFile.spc  
```  
  
## <a name="see-also"></a>関連項目  
 [.NET Framework ツール](../../../docs/framework/tools/index.md)   
 [Makecert.exe (証明書作成ツール)](http://msdn.microsoft.com/library/b0343f8e-9c41-4852-a85c-f8a0c408cf0d)   
 [Visual Studio 用開発者コマンド プロンプト](../../../docs/framework/tools/developer-command-prompt-for-vs.md)


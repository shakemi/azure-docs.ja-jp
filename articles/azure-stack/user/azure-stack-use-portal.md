---
title: Azure Stack ポータルの使用 | Microsoft Docs
description: Azure Stack でユーザー ポータルにアクセスして使用する方法を説明します。
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 5aa00123-5b87-45e0-a671-4165e66bfbc6
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2018
ms.author: mabrigg
ms.openlocfilehash: 279722cc53889cb0a261fcffde0c7e0f86be6dc5
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="using-the-azure-stack-portal"></a>Azure Stack ポータルの使用

*適用先: Azure Stack 統合システムと Azure Stack 開発キット*

Azure Stack サービスのコンシューマーは Azure Stack ポータルを使用して、パブリック プランをサブスクライブしたり、これらのプランで提供されるサービスを使用したりできます。 以前に Azure ポータルを使用したことがある場合、ユーザー インターフェースには既に慣れています。

## <a name="access-the-portal"></a>ポータルへのアクセス

Azure Stack オペレーター (サービス プロバイダーまたは組織内の管理者のどちらか) から、ポータルにアクセスするための正しい URL が通知されます。

- 統合システムの場合、URL はオペレーターのリージョンと外部ドメイン名によって異なり、https://portal.&lt;*リージョン*&gt;.&lt;*FQDN*&gt; の形式になります。
- Azure Stack Development Kit を使用している場合、ポータルのアドレスは https://portal.local.azurestack.external になります。

![Azure Stack ユーザー ポータルのスクリーンショット](media/azure-stack-use-portal/UserPortal.png)

## <a name="customize-the-dashboard"></a>ダッシュボードのカスタマイズ

ダッシュボードには、タイルの既定のセットが含まれています。 **[ダッシュボードの編集]** をクリックして既定のダッシュボードを変更したり、**[新しいダッシュボード]** をクリックしてカスタムのダッシュボードを作成したりできます。 タイルを追加または削除して、ダッシュボードを簡単にカスタマイズすることができます。 たとえば、コンピューティング タイルを追加するには、**[新規]** をクリックします。 **[コンピューティング]** を右クリックし、**[ダッシュボードにピン留め]** をクリックします。

## <a name="create-subscription-and-browse-available-resources"></a>サブスクリプションの作成と使用可能リソースの参照
 
まだサブスクリプションがない場合、まずオファーをサブスクライブする必要があります。 その後、利用可能なリソースを参照することができます。 リソースを参照したり作成したりするには、次のいずれかの方法を使用します。

- ダッシュボードで **[Marketplace] (マーケットプレース)** タイルをクリックします。
- **[All resources] (すべてのリソース)** タイルで、**[Create resources] (リソースの作成)** をクリックします。
- 左側のナビゲーション ウィンドウで、 **[New] (新規)** をクリックします。

## <a name="learn-how-to-use-available-services"></a>使用可能なサービスの使用方法を学ぶ

使用可能なサービスの使用方法についてガイダンスが必要な場合に、利用できるオプションが異なる可能性があります。

- 組織またはサービス プロバイダーによって独自のドキュメントが提供されることがあります。これは通常、カスタマイズされたサービスまたはアプリが提供される場合です。
- サード パーティのアプリには、独自のドキュメントがあります。
- Azure 互換サービスについては、まず Azure Stack のドキュメントを確認することを強くお勧めします。 Azure Stack ユーザー ドキュメントにアクセスするには、[Help] (ヘルプ) アイコンをクリックしてから、**[Help + support] (ヘルプとサポート)** をクリックします。
 
    ![UI の [Help and support] (ヘルプとサポート) オプションのスクリーンショット](media/azure-stack-use-portal/HelpAndSupport.png)

    特に、作業を開始するにあたって次の記事を確認することをお勧めします。

    - [主な考慮事項: Azure Stack でのサービスの使用またはアプリの作成](azure-stack-considerations.md)
    - ドキュメントのサービスの使用に関するセクションには、サービスごとの "考慮事項" の記事があります。 "考慮事項" に関するページでは、Azure で提供されるサービスと Azure Stack で提供される同じサービス間の相違点を説明しています。 例については、「[VM に関する考慮事項](azure-stack-vm-considerations.md)」を参照してください。 「Use services (サービスの使用)」セクションには、Azure Stack に固有であるその他の情報が含まれている場合があります。
     
      サービスの一般的なリファレンスとして Azure のドキュメントを使用できますが、これらの相違点を把握しておく必要があります。 **[Quickstart tutorials] (クイックスタート チュートリアル)** タイル上のドキュメント リンクが Azure のドキュメントを指していることを理解します。

## <a name="get-support"></a>サポートを受ける

追加のサポートが必要な場合は、所属組織またはサービス プロバイダーにお問い合わせください。

Azure Stack Development Kit を使用している場合、[Azure Stack フォーラム](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)が唯一のサポート情報源です。

## <a name="next-steps"></a>次の手順

[主な考慮事項: Azure Stack でのサービスの使用またはアプリの作成](azure-stack-considerations.md)

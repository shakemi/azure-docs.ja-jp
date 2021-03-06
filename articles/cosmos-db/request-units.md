---
title: 要求ユニットとスループットの推定 - Azure Cosmos DB | Microsoft Docs
description: Azure Cosmos DB の要求ユニット要件を確認、指定、推定する方法について説明します。
services: cosmos-db
author: SnehaGunda
manager: kfile
documentationcenter: ''
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/09/2018
ms.author: rimman
ms.openlocfilehash: 2b69b3b5fee0d1148a762f817d9c5a8bc67806e7
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2018
---
# <a name="request-units-in-azure-cosmos-db"></a>Azure Cosmos DB の要求ユニット

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) は、Microsoft が提供するグローバル分散型のマルチモデル データベースです。 Azure Cosmos DB では、仮想マシンのレンタル、ソフトウェアのデプロイ、データベースの監視などを自分で行う必要はありません。 Microsoft のトップ エンジニアによって運用され、継続的な監視が行われる Azure Cosmos DB は、卓越した可用性、パフォーマンス、データ保護を提供します。 [SQL API](documentdb-introduction.md)、[MongoDB API](mongodb-introduction.md)、[Table API](table-introduction.md)、[Gremlin API](graph-introduction.md) を介したグラフなど、お好きな API を利用してデータへアクセスできます。こうした API はすべてネイティブにサポートされています。 

Azure Cosmos DB の通貨は**要求ユニット (RU)** です。 RU を使用すると、読み取り、書き込み容量の予約や、CPU、メモリ、および IOPS のプロビジョニングが不要です。 Azure Cosmos DB は、単純な読み取りと書き込みから複雑なグラフのクエリまで、さまざまな操作を行うための API を多数サポートしています。 すべての要求が同等ではないため、要求を処理するために必要な計算量に基づいて、正規化された**要求ユニット**の量が割り当てられます。 1 つの操作の要求ユニットの数は確定的であり、Azure Cosmos DB のすべての操作で使用された要求ユニットの数は応答ヘッダーを介して追跡できます。 

予測可能性を高めるには、100 RU/秒単位でスループットを予約する必要があります。 Azure Cosmos DB の[要求ユニット計算ツール](https://www.documentdb.com/capacityplanner)を使って、[スループットのニーズを推定する](request-units.md#estimating-throughput-needs)ことができます。

![Throughput calculator][5]

この記事を読むと、次の質問に回答できるようになります。  

* Azure Cosmos DB の要求ユニットと要求の使用量とは何ですか。
* Azure Cosmos DB のコンテナーの要求ユニットの容量はどのように指定しますか。
* アプリケーションの要求ユニットのニーズをどのように推定しますか。
* Azure Cosmos DB のコンテナーの要求ユニットの容量を超えた場合はどうなりますか?

Azure Cosmos DB は複数モデルのデータベースです。この記事は、Azure Cosmos DB のすべてのデータ モデルと API に適用されることに注意してください。 この記事では、*コンテナー*、*項目*などの一般的な用語を使用して、コレクション、グラフ、テーブル、ドキュメント、ノード、エンティティをそれぞれ一般的に参照します。

## <a name="request-units-and-request-charges"></a>要求ユニットと要求の使用量
Azure Cosmos DB を使用して、アプリケーションのスループット ニーズを満たすリソースを "*予約*" することで、高速の予測可能なパフォーマンスが得られます。  アプリケーション負荷とアクセス パターンは時間と共に変化するため、Azure Cosmos DB はアプリケーションで利用できる予約済みスループットの量を簡単に増減できる機能を備えています。

Azure Cosmos DB では、1 秒で処理する要求ユニットで、予約済みスループットを指定します。 要求ユニットはスループットの通貨と考えることができます。この通貨によって、アプリケーションで利用できる保証された要求ユニット量を秒単位で "*予約*" できます。  ドキュメントの作成、クエリの実行、ドキュメントの更新など、Azure Cosmos DB での各操作は、CPU、メモリ、IOPS を消費します。  つまり、それぞれの操作により、"*要求の使用量*" が発生し、それが "*要求ユニット*" で表されます。  アプリケーションのスループット要件と共に、要求ユニット使用量に影響を及ぼす要因を理解しておくと、できるだけコスト効率の高い方法でアプリケーションを実行できます。 また、Azure Portal のデータ エクスプローラーは、クエリの核となる部分をテストできるすばらしいツールでもあります。

Azure Cosmos DB プログラム マネージャーの Andrew Liu が要求単位について説明する次のビデオを最初に見ることをお勧めします。

> [!VIDEO https://www.youtube.com/embed/stk5WSp5uX0]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Azure Cosmos DB での要求ユニット量の指定
新しいコンテナーを開始するときに、予約する 1 秒あたりの要求ユニット数 (RU/秒) を指定します。 プロビジョニング済みのスループットに基づいて、Azure Cosmos DB はコンテナーをホストする物理パーティションを割り当て、データの増加に応じてパーティション間でデータの分割やバランスの再調整を行います。

Azure Cosmos DB コンテナーは、固定または無制限として作成することができます。 固定サイズのコンテナーの上限は、容量が 10 GB で、スループットが毎秒 10,000 RU となります。 無制限のコンテナーを作成する場合は、最低でも 1,000 RU/秒のスループットと[パーティション キー](partition-data.md)を指定する必要があります。 データが複数のパーティションに分割される場合があるため、高基数 (100 ～数百万の個別の値) のパーティション キーを選択する必要があります。 多数の異なる値を持つパーティション キーを選択すると、コンテナー/テーブル/グラフおよび要求を、Azure Cosmos DB で確実かつ一様に拡大縮小できるようになります。 

> [!NOTE]
> パーティション キーは論理境界であり、物理的な境界ではありません。 したがって、個別のパーティション キー値の数を制限する必要はありません。 Azure Cosmos DB には他にも負荷分散のオプションがあるので、個別のパーティション キー値は多くしておくことをお勧めします。

次に示すコード スニペットは、.NET SDK を使用して、1 秒あたり 3,000 要求ユニットのコンテナーを作成します。

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB は、スループットの予約モデルで運用されます。 つまり、実際に "*使用した*" スループット量ではなく、"*予約した*" スループット量に対する料金が請求されます。 アプリケーションの負荷やデータ、使用パターンが変化したときは、SDK や [Azure Portal](https://portal.azure.com) を使用して、予約済み RU の量を簡単にスケールアップしたりスケールダウンしたりできます。

各コンテナーは、Azure Cosmos DB の `Offer` リソースにマップされます。このリソースは、プロビジョニング済みスループットに関するメタデータを持っています。 割り当て済みのスループットを変更するには、コンテナーに対応する Offer リソースを検索して、新しいスループット値に更新します。 次に示すコード スニペットは、.NET SDK を使用して、コンテナーのスループットを 1 秒あたり 5,000 要求ユニットに変更します。

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

スループットを変更しても、コンテナーの可用性には影響しません。 通常、新しく予約されたスループットは、数秒後にアプリケーションで有効になります。

## <a name="throughput-isolation-in-globally-distributed-databases"></a>グローバルな分散型データベースのスループット分離

データベースを複数のリージョンにレプリケートした場合、Azure Cosmos DB はスループット分離を提供することで、あるリージョンの RU の使用が、別のリージョンの RU の使用状況に影響を及ぼさないようにします。 たとえば、あるリージョンにデータを書き込み、別のリージョンからデータを読み取る場合、リージョン *A* の書き込み操作の実行に使用された RU によって、リージョン *B* の読み取り操作に使用された RU の機能が低下することはありません。RU は、デプロイした複数のリージョンの枠を越えては分割されません。 データベースがレプリケートされた各リージョンには、RU の全容量がプロビジョニングされます。 グローバル レプリケーションの詳細については、「[Azure Cosmos DB を使用してデータをグローバルに分散させる方法](distribute-data-globally.md)」をご覧ください。

## <a name="request-unit-considerations"></a>要求ユニットの考慮事項
Azure Cosmos DB コンテナー用にプロビジョニングする要求ユニット数を推定する際は、以下の変数についても検討することが重要です。

* **アイテムのサイズ**。 サイズが増大すると、データの読み取りまたは書き込みに使用される要求単位数も増加します。
* **アイテム プロパティの数**。 すべてのプロパティに既定でインデックスが作成されると想定すると、プロパティ数の増加に伴って、ドキュメント/ノード/エンティティの書き込みに使用される単位が増加します。
* **データ整合性**。 Strong または Bounded Staleness のデータの整合性モデルを使用すると、アイテムの読み取りに使用される要求単位が増加します。
* **インデックス付きプロパティ**。 各コンテナーのインデックス ポリシーによって、既定でインデックスが作成されるプロパティが決まります。 インデックス付きプロパティの数を制限するか、非同期インデックス作成を有効にして、使用する要求ユニットを削減できます。
* **ドキュメントのインデックス作成**。 既定では、アイテムごとにインデックスが自動的に作成されます。 一部のアイテムにインデックスを作成しないようにすると、使用される要求ユニットが少なくなります。
* **クエリのパターン**。 クエリの複雑さは、操作で消費される要求ユニット数に影響します。 述語の数、述語の特性、プロジェクション、UDF 数、ソース データのサイズのすべてが、クエリ操作のコストに影響します。
* **スクリプトの使用**。  クエリと同様に、ストアド プロシージャとトリガーは、実行する操作の複雑さに基づいて要求ユニットを使用します。 アプリケーションを開発するときは、ヘッダーを調べて、各操作で使用される要求単位の量を詳しく把握するようにしてください。

## <a name="estimating-throughput-needs"></a>スループットのニーズの推定
要求単位は、要求の処理コストを標準化した測定単位です。 1 つの要求ユニットは、10 個の一意のプロパティ値 (システム プロパティを除く) で構成される 1 KB のアイテムの読み取り (self リンクまたは ID による) に必要な処理能力を表します。 同じアイテムを作成 (挿入)、置換、または削除する要求では、必要になるサービスの処理が多くなるため、使用される要求ユニットも多くなります。   

> [!NOTE]
> 1 KB のアイテムに対する 1 つの要求ユニットのベースラインは、アイテムのセルフ リンクまたは ID による単純な GET に対応します。
> 
> 

たとえば、次の表は、3 種類のサイズのアイテム (1 KB、4 KB、64 KB) を 2 種類のパフォーマンス レベル (500 読み取り/秒 + 100 書き込み/秒と、500 読み取り/秒 + 500 書き込み/秒) でプロビジョニングした場合の要求ユニット数を示しています。 データの一貫性は*セッション*で構成され、インデックス作成ポリシーは*なし*に設定されています。

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>アイテムのサイズ</strong></p></td>
            <td valign="top"><p><strong>読み取り数/秒</strong></p></td>
            <td valign="top"><p><strong>書き込み数/秒</strong></p></td>
            <td valign="top"><p><strong>要求ユニット</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1,000 RU/秒</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3,000 RU/秒</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1.3) + (100 * 7) = 1,350 RU/秒</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1.3) + (500 * 7) = 4,150 RU/秒</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9,800 RU/秒</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29,000 RU/秒</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a>要求ユニット計算ツールの使用
スループットをユーザーが緻密に推定できるように、Web ベースの[要求ユニット計算ツール](https://www.documentdb.com/capacityplanner)が用意されています。たとえば以下に示す標準的な操作で必要になる要求ユニットを見積もることができます。

* アイテムの作成 (書き込み)
* アイテムの読み取り
* アイテムの削除
* アイテムの更新

このツールには、指定したサンプル アイテムに基づいたデータ ストレージ ニーズの見積もりのサポートも含まれています。

ツールの使い方は簡単です。

1. 代表的なアイテム (サンプルの JSON ドキュメントなど) を少なくとも 1 つアップロードします。
   
    ![要求ユニット計算ツールへのアイテムのアップロード][2]
2. データ ストレージの要件を見積もるには、格納するアイテム (ドキュメント、テーブル、グラフなど) の総数を入力します。
3. 作成、読み取り、更新、削除に関して必要な操作数 (毎秒あたり) を入力します。 アイテムの更新操作の要求ユニットの料金を見積もるには、上記の手順 1. のサンプル アイテムのうち、代表的なフィールドの更新が含まれているアイテムのコピーをアップロードします。  たとえば、アイテムの更新では、通常、*lastLogin* と *userVisits* という 2 つのプロパティだけを変更する場合は、サンプル アイテムをコピーし、その 2 つのプロパティの値を更新して、コピーしたアイテムをアップロードします。
   
    ![Enter throughput requirements in the request unit calculator][3]
4. 計算ボタンをクリックして結果を確認します。
   
    ![Request unit calculator results][4]

> [!NOTE]
> アイテムの種類によって、サイズとインデックス付きプロパティの数が大きく異なる場合は、それぞれの "*種類*" における代表的なアイテムのサンプルをツールにアップロードしたうえで、結果を計算してください。
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a>Azure Cosmos DB の "要求の使用量" 応答ヘッダーの使用
Azure Cosmos DB サービスからの各応答には、特定の要求で使用される要求ユニットを含むカスタム ヘッダー (`x-ms-request-charge`) が付きます。 このヘッダーには、Azure Cosmos DB SDK を介してアクセスすることもできます。 .NET SDK で、`RequestCharge` は `ResourceResponse` オブジェクトのプロパティです。  Azure Portal の Azure Cosmos DB データ エクスプローラーは、実行されたクエリに関する要求の使用量情報を示します。

これを踏まえて、アプリケーションに必要な予約済みスループットの量を推定するには、典型的な操作の実行に関連する要求ユニット使用量を記録し、アプリケーションが使用する代表的なアイテムに基づいて、1 秒ごとに実行される操作数を推定します。  さらに、通常のクエリと Azure Cosmos DB スクリプトの使用も忘れずに測定し、考慮に入れます。

> [!NOTE]
> アイテムの種類によって、サイズとインデックス付きプロパティの数が大きく異なる場合は、典型的なアイテムの "*種類*" ごとに、適用可能な操作の要求ユニット使用量を記録してください。
> 
> 

例: 

1. 典型的なアイテム作成 (挿入) の要求ユニット使用量を記録します。 
2. 典型的なアイテム読み取りの要求ユニット使用量を記録します。
3. 典型的なアイテム更新の要求ユニット使用量を記録します。
4. 典型的な共通アイテムのクエリの要求ユニット使用量を記録します。
5. アプリケーションが利用するカスタム スクリプト (ストアド プロシージャ、トリガー、ユーザー定義関数) の要求ユニット使用量を記録します。
6. 予想される 1 秒あたりの操作実行数の推定値に基づいて、必要な要求ユニットを計算します。

## <a name="a-request-unit-estimate-example"></a>要求ユニット推定の例
次の 1 KB 未満のドキュメントについて考えてみましょう。

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> ドキュメントは Azure Cosmos DB で縮小されるため、システムで計算される上記ドキュメントのサイズは 1 KB をわずかに下回ります。
> 
> 

次の表は、このアイテムに対する典型的な操作に要する、大まかな要求ユニット使用量を示しています (大まかな要求ユニット使用量は、アカウント一貫性レベルが *セッション* に設定され、すべてのアイテムに自動でインデックス作成が行われることを想定しています)。

| 操作 | 要求ユニット使用量 |
| --- | --- |
| アイテムを作成する |～15 RU |
| アイテムの読み取り |～1 RU |
| ID でのアイテムのクエリ |～2.5 RU |

さらに次の表では、アプリケーションで通常使用されるクエリについて、大まかな要求ユニット使用量を示しています。

| クエリ | 要求ユニット使用量 | 返されるアイテム数 |
| --- | --- | --- |
| ID で食品を選択 |～2.5 RU |1 |
| 製造者で食品を選択 |～7 RU |7 |
| 食品グループで選択し、重量順に配列 |～70 RU |100 |
| 食品グループの上位 10 食品を選択 |～10 RU |10 |

> [!NOTE]
> RU 使用量は返されるアイテムの数により異なります。
> 
> 

この情報があれば、予測される 1 秒あたりの操作数とクエリ数に基づいて、このアプリケーションに必要な RU 要件を推定できます。

| 操作/クエリ | 1 秒あたりの推定数 | 必要な RU |
| --- | --- | --- |
| アイテムを作成する |10 |150 |
| アイテムの読み取り |100 |100 |
| 製造者で食品を選択 |25 |175 |
| 食品グループで選択 |10 |700 |
| 上位 10 を選択 |15 |合計 150 |

この例では、平均スループット要件を 1,275 RU/s と想定しています。  100 の位で丸めて、このアプリケーションのコンテナーに 1,300 RU/s をプロビジョニングすることになります。

## <a id="RequestRateTooLarge"></a> Azure Cosmos DB での予約されたスループット上限の超過
要求ユニットの消費は、1 秒あたりのレートとして評価されることを思い出してください。 プロビジョニング済み要求ユニット レートを超過したアプリケーションの場合、レートがプロビジョニング済みスループット レベルを下回るまで、要求のレートが制限されます。 要求のレートが制限される場合、サーバーはいち早く `RequestRateTooLargeException` (HTTP 状態コード 429) で要求を終了させ、`x-ms-retry-after-ms` ヘッダーを返して、ユーザーが要求の試行を再開できるまでに待機しなければならない時間をミリ秒で示します。

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

.NET クライアント SDK と LINQ クエリ使用していると、ほとんどの場合は、この例外に対処する必要がありません。最新バージョンの .NET クライアント SDK は暗黙的にこの応答を取得し、サーバーが規定した retry-after ヘッダーを考慮して、要求を自動的に再試行するからです。 アカウントに複数のクライアントが同時アクセスしている状況でなければ、次回の再試行は成功します。

複数のクライアントが上述の要求レートで累積的に操作を実行している場合は、既定の再試行動作では十分な結果が得られず、クライアントは状態コード 429 で `DocumentClientException` をアプリケーションにスローします。 こうした場合は、再試行動作とアプリケーションのエラー処理ルーチンのロジックを制御するか、対象コンテナーのプロビジョニング済みスループットを増やすことを検討します。

## <a name="next-steps"></a>次の手順
Azure Cosmos DB データベースの予約済みスループットの詳細については、以下のリソースを参照してください。

* [Azure Cosmos DB の価格](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Azure Cosmos DB でのデータのパーティション分割](partition-data.md)

Azure Cosmos DB の詳細については、Azure Cosmos DB の[ドキュメント](https://azure.microsoft.com/documentation/services/cosmos-db/)を参照してください。 

Azure Cosmos DB に関するスケールとパフォーマンスのテストを始めるには、「[Azure Cosmos DB のパフォーマンスとスケールのテスト](performance-testing.md)」を参照してください。

[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png

---
title: Azure SQL Database - レプリカでの読み取りクエリ | Microsoft Docs
description: Azure SQL Database は、読み取りスケールアウトと呼ばれる読み取り専用レプリカの容量を使用して、読み取り専用ワークロードを負荷分散する機能を提供します。
services: sql-database
author: anosov1960
manager: craigg
ms.service: sql-database
ms.custom: monitor & tune
ms.topic: article
ms.date: 04/17/2018
ms.author: sashan
ms.openlocfilehash: 6e82b851f7dc7e2b8c7fe996bff843c8f10f2978
ms.sourcegitcommit: 59914a06e1f337399e4db3c6f3bc15c573079832
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="use-read-only-replicas-to-load-balance-read-only-query-workloads-preview"></a>読み取り専用レプリカを使用して読み取り専用クエリ ワークロードを負荷分散する (プレビュー)

**読み取りスケールアウト**では、読み取り専用レプリカの容量を使用して、Azure SQL Database の読み取り専用ワークロードを負荷分散できます。 

## <a name="overview-of-read-scale-out"></a>読み取りスケールアウトの概要

Premium 階層 ([DTU ベースの購入モデル](sql-database-service-tiers.md#dtu-based-purchasing-model)) または Business Critical 階層 ([仮想コアベースの購入モデル](sql-database-service-tiers.md#vcore-based-purchasing-model-preview)) の各データベースは、可用性 SLA をサポートするために、複数の Always ON レプリカによって自動的にプロビジョニングされます。 これらのレプリカは、通常のデータベース接続で使用される読み取り/書き込みレプリカと同じパフォーマンス レベルでプロビジョニングされます。 **読み取りスケールアウト**機能では、読み取り/書き込みレプリカを共有する代わりに、読み取り専用レプリカの容量を使用して SQL Database の読み取り専用ワークロードを負荷分散できます。 これにより、読み取り専用ワークロードがメインの読み取り/書き込みワークロードから分離され、パフォーマンスに影響を与えなくなります。この機能は、分析などの論理的に分離された読み取り専用ワークロードを含むアプリケーションを対象としているため、追加のコストをかけずに追加容量を使用できるというパフォーマンス上のメリットが得られます。

特定のデータベースで読み取りスケールアウト機能を使用するには、データベースを作成するときに明示的に有効にするか、PowerShell を使用して [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) または [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) コマンドレットを呼び出すか、Azure Resource Manager REST API から[データベース - 作成または更新](/rest/api/sql/databases/createorupdate)メソッドを使用して構成を変更し、後から明示的に有効にする必要があります。 

データベースの読み取りスケールアウトが有効になると、そのデータベースに接続するアプリケーションが、アプリケーションの接続文字列で構成されている `ApplicationIntent` プロパティに応じて、データベースの読み取り/書き込みレプリカまたは読み取り専用レプリカにリダイレクトされます。 `ApplicationIntent` プロパティの詳細については、「[アプリケーションの目的を指定する](https://docs.microsoft.com/sql/relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery#specifying-application-intent)」を参照してください。

> [!NOTE]
> プレビュー中は、読み取り専用レプリカでのクエリ データ ストアと拡張イベントはサポートされません。

## <a name="data-consistency"></a>データの一貫性

Alwasy ON のメリットの 1 つは、レプリカが常にトランザクション上一貫性が保たれた状態となることですが、さまざまな時点で異なるレプリカ間に短い待機時間が発生する可能性があります。 読み取りスケールアウトは、セッション レベルの一貫性をサポートしています。 そのため、レプリカが使用できないことが原因で接続エラーが発生した後に読み取り専用セッションが再接続された場合、読み取り/書き込みレプリカを使用して 100% 最新ではないレプリカにリダイレクトされる可能性があります。 同様に、アプリケーションが読み取り/書き込みセッションを使用してデータを書き込み、読み取り専用セッションを使用してすぐに読み取る場合、最新の更新がすぐに表示されない可能性があります。 これは、レプリカへのトランザクション ログの再実行が非同期であるためです。

> [!NOTE]
> 領域内のレプリケーションの待機時間は短く、このような状況はまれです。


## <a name="connecting-to-a-read-only-replica"></a>読み取り専用レプリカに接続する

データベースの読み取りスケールアウトを有効にすると、クライアントによって提供された接続文字列の `ApplicationIntent` オプションにより、接続が書き込みレプリカと読み取り専用レプリカのどちらにルーティングされるかが指定されます。 具体的には、`ApplicationIntent` 値が `ReadWrite` (既定値) の場合、接続はデータベースの読み取り/書き込みレプリカにリダイレクトされます。 これは、既存の動作と同じです。 `ApplicationIntent` 値が `ReadOnly` の場合、接続は読み取り可能レプリカにルーティングされます。

たとえば、次の接続文字列はクライアントを読み取り専用レプリカに接続します (山かっこ内の項目は環境内の適切な値に置き換え、山かっこは削除します)。

```SQL
Server=tcp:<server>.database.windows.net;Database=<mydatabase>;ApplicationIntent=ReadOnly;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;
```

次の接続文字列はどちらもクライアントを読み取り/書き込みレプリカに接続します (山かっこ内の項目は環境内の適切な値に置き換え、山かっこは削除します)。

```SQL
Server=tcp:<server>.database.windows.net;Database=<mydatabase>;ApplicationIntent=ReadWrite;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;

Server=tcp:<server>.database.windows.net;Database=<mydatabase>;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;
```

## <a name="enable-and-disable-read-scale-out-using-azure-powershell"></a>Azure PowerShell を使用して読み取りスケールアウトを有効または無効にする

Azure PowerShell で読み取りスケールアウトを管理するには、2016 年 12 月以降のリリースの Azure PowerShell が必要です。 最新の PowerShell リリースについては、[Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) に関するページを参照してください。

Azure PowerShell で [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) コマンドレットを呼び出し、`-ReadScale` パラメーターに目的の値 (`Enabled` または `Disabled`) を渡して、読み取りスケールアウトを有効または無効にします。 または、[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) コマンドレットを使用して、読み取りスケールアウトが有効になっている新しいデータベースを作成することもできます。

たとえば、既存のデータベースの読み取りスケールアウトを有効にするには、次のようにします (山かっこ内の項目は環境内の適切な値に置き換え、山かっこは削除します)。

```powershell
Set-AzureRmSqlDatabase -ResourceGroupName <myresourcegroup> -ServerName <myserver> -DatabaseName <mydatabase> -ReadScale Enabled
```

既存のデータベースの読み取りスケールアウトを無効にするには、次のようにします (山かっこ内の項目は環境内の適切な値に置き換え、山かっこは削除します)。

```powershell
Set-AzureRmSqlDatabase -ResourceGroupName <myresourcegroup> -ServerName <myserver> -DatabaseName <mydatabase> -ReadScale Disabled
```

読み取りスケールアウトが有効になっている新しいデータベースを作成するには、次のようにします (山かっこ内の項目は環境内の適切な値に置き換え、山かっこは削除します)。

```powershell
New-AzureRmSqlDatabase -ResourceGroupName <myresourcegroup> -ServerName <myserver> -DatabaseName <mydatabase> -ReadScale Enabled -Edition Premium
```

## <a name="enabling-and-disabling-read-scale-out-using-the-azure-sql-database-rest-api"></a>Azure SQL Database REST API を使用して読み取りスケールアウトを有効または無効にする

読み取りスケールアウトが有効になっているデータベースを作成したり、既存のデータベースの読み取りスケールアウトを有効または無効にしたりするには、次の要求のサンプルのように `readScale` プロパティを `Enabled` または `Disabled` に設定して、対応するデータベース エンティティを作成または更新します。

```rest
Method: PUT
URL: https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{GroupName}/providers/Microsoft.Sql/servers/{ServerName}/databases/{DatabaseName}?api-version= 2014-04-01-preview
Body:
{
   "properties":
   {
      "readScale":"Enabled"
   }
} 
```

詳細については、「[データベース - 作成または更新](/rest/api/sql/databases/createorupdate)」を参照してください。

## <a name="next-steps"></a>次の手順

- PowerShell を使用した読み取りスケールアウトの設定の詳細については、「[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)」コマンドレットまたは「[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)」コマンドレットを参照してください。
- REST API を使用した読み取りスケールアウトの設定の詳細については、「[データベース - 作成または更新](/rest/api/sql/databases/createorupdate)」を参照してください。

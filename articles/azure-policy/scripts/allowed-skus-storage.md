---
title: Azure Policy の JSON サンプル - ストレージ アカウントおよび仮想マシンに対して許可されている SKU | Microsoft Docs
description: この JSON サンプル ポリシーは、承認された SKU がストレージ アカウントと仮想マシンで使用されていることが要件です。
services: azure-policy
documentationcenter: ''
author: DCtheGeek
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: azure-policy
ms.devlang: ''
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: ''
ms.date: 10/30/2017
ms.author: dacoulte
ms.custom: mvc
ms.openlocfilehash: a86e6ae1b12c59b0f103ec2bce1ec86ef3fa5146
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
---
# <a name="allowed-skus-for-storage-accounts-and-virtual-machines"></a>ストレージ アカウントおよび仮想マシンに対して許可されている SKU

このポリシーは、承認された SKU がストレージ アカウントと仮想マシンで使用されていることが要件です。 組み込みのポリシーを使用して、承認された SKU を確認します。 承認された仮想マシンの SKU の配列と、承認されたストレージ アカウントの SKU の配列を指定します。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>サンプル テンプレート

[!code-json[main](../../../policy-templates/samples/PolicyInitiatives/skus-for-mutiple-types/azurepolicyset.json "Allowed SKUs for Storage Accounts and Virtual Machines")]

このテンプレートは、[Azure Portal](#deploy-with-the-portal) または [PowerShell](#deploy-with-powershell) を使用してデプロイできます。

## <a name="deploy-with-the-portal"></a>ポータルでのデプロイ

[![Azure へのデプロイ](http://azuredeploy.net/deploybutton.png)](https://aka.ms/getpolicy)

## <a name="deploy-with-powershell"></a>PowerShell でデプロイする

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$policydefinitions = "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/skus-for-mutiple-types/azurepolicyset.definitions.json"
$policysetparameters = "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/skus-for-mutiple-types/azurepolicyset.parameters.json"

$policyset= New-AzureRmPolicySetDefinition -Name "skus-for-mutiple-types" -DisplayName "Allowed SKUs for Storage Accounts and Virtual Machines" -Description "This policy allows you to speficy what skus are allowed for storage accounts and virtual machines" -PolicyDefinition $policydefinitions -Parameter $policysetparameters

New-AzureRmPolicyAssignment -PolicySetDefinition $policyset -Name <assignmentname> -Scope <scope>  -LISTOFALLOWEDSKUS_1 <VM SKUs> -LISTOFALLOWEDSKUS_2 <Storage Account SKUs >  -Sku @{"Name"="A1";"Tier"="Standard"}
```

### <a name="clean-up-powershell-deployment"></a>PowerShell でのデプロイをクリーンアップする

次のコマンドを実行して、リソース グループ、VM、すべての関連リソースを削除します。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>次の手順

- その他の Azure Policy テンプレートのサンプルについては、「[Templates for Azure Policy (Azure Policy のテンプレート)](../json-samples.md)」を参照してください。

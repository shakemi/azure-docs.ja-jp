---
title: Azure クイック スタート - CLI で VM を作成する | Microsoft Docs
description: Azure CLI で仮想マシンを作成する方法を簡単に説明します。
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/13/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 15dc70e8d60901b71ba7d1d9333b13d8266d18c6
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2018
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a>Azure CLI で Linux 仮想マシンを作成する

Azure CLI は、コマンドラインやスクリプトで Azure リソースを作成および管理するために使用します。 このクイックスタートでは、Azure CLI を使用して、Ubuntu Server を実行する仮想マシンをデプロイする方法について詳しく説明します。 サーバーのデプロイ後、SSH 接続を作成し、NGINX Web サーバーをインストールします。

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) を作成してください。

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI をローカルにインストールして使用する場合、このクイック スタートを実施するには、Azure CLI バージョン 2.0.4 以降を実行している必要があります。 バージョンを確認するには、`az --version` を実行します。 インストールまたはアップグレードする必要がある場合は、「[Azure CLI 2.0 のインストール]( /cli/azure/install-azure-cli)」を参照してください。 

## <a name="create-a-resource-group"></a>リソース グループの作成

[az group create](/cli/azure/group#az_group_create) コマンドでリソース グループを作成します。 Azure リソース グループとは、Azure リソースのデプロイと管理に使用する論理コンテナーです。 

次の例では、*myResourceGroup* という名前のリソース グループを *eastus* に作成します。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>仮想マシンの作成

[az vm create](/cli/azure/vm#az_vm_create) コマンドで VM を作成します。 

次の例では、*myVM* という名前の VM を作成し、*azureuser* という名前のユーザー アカウントを追加して、既定のキーの場所 (*~/.ssh*) にまだ SSH キーが存在しない場合は SSH キーを生成します。 特定のキーのセットを使用するには、`--ssh-key-value` オプションを使用します。

```azurecli-interactive
az vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

VM が作成されると、Azure CLI によって次の例のような情報が表示されます。 `publicIpAddress` を書き留めておきます。 このアドレスは、VM へのアクセスに使用されます。

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Web トラフィック用にポート 80 を開く 

Azure にデプロイされている Linux 仮想マシンに対しては、既定で SSH 接続のみが許可されます。 この VM を Web サーバーとして使用する場合は、インターネットからポート 80 を開く必要があります。 [az vm open-port](/cli/azure/vm#az_vm_open_port) コマンドを使用して、目的のポートを開きます。  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>VM への SSH 接続

次のコマンドを使用して、仮想マシンとの SSH セッションを作成します。 **publicIpAddress** は、仮想マシンの正しいパブリック IP アドレスに置き換えてください。  上記の例の IP アドレスは *40.68.254.142* でした。

```bash 
ssh publicIpAddress
```

## <a name="install-nginx"></a>NGINX のインストール

次のコマンドを使用して、パッケージ ソースを更新し、最新の NGINX パッケージをインストールします。 

```bash 
# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a>NGINX のようこそページの表示

NGINX をインストールし、VM のポート 80 をインターネットから開いたら、任意の Web ブラウザーを使用して NGINX の既定のようこそページを表示することができます。 上の手順で指定した *publicIpAddress* を使用して既定のページにアクセスします。 

![NGINX の既定のサイト](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>リソースのクリーンアップ

必要がなくなったら、[az group delete](/cli/azure/group#az_group_delete) コマンドを使用して、リソース グループ、VM、およびすべての関連リソースを削除できます。 VM への SSH セッションを終了し、次の手順でリソースを削除します。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>次の手順

このクイック スタートでは、単純な仮想マシンとネットワーク セキュリティ グループの規則をデプロイし、Web サーバーをインストールしました。 Azure 仮想マシンの詳細については、Linux VM のチュートリアルを参照してください。


> [!div class="nextstepaction"]
> [Azure Linux 仮想マシンのチュートリアル](./tutorial-manage-vm.md)

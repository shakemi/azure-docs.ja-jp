---
title: Azure Active Directory B2C テナントの作成 | Microsoft Docs
description: Azure Active Directory B2C テナントの作成方法に関するトピック
services: active-directory-b2c
documentationcenter: ''
author: davidmu1
manager: mtillman
editor: ''
ms.service: active-directory-b2c
ms.workload: identity
ms.topic: article
ms.date: 06/07/2017
ms.author: davidmu
ms.openlocfilehash: 56e0ae7454e86911c894da88b5aa8ccc03a08af3
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a>Azure Portal で Azure Active Directory B2C テナントを作成する

このクイック スタートを読むと、Microsoft Azure Active Directory (Azure AD) B2C テナントを数分で作成できるようになります。 完了したら、B2C アプリケーションの登録で使用する B2C テナント (ディレクトリとも言います) ができます。

## <a name="prerequisites"></a>前提条件

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a>Azure にログインする

[Azure Portal](https://portal.azure.com/) にログインします。

## <a name="create-an-azure-ad-b2c-tenant"></a>Azure AD B2C テナントを作成する

既存のテナントで B2C の機能を有効にすることはできません。 Azure AD B2C テナントを作成する必要があります。

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

おめでとうございます、Azure Active Directory B2C テナントが作成されました。 あなたはこのテナントのグローバル管理者です。 必要に応じて、他のグローバル管理者を追加できます。 新しいテナントに切り替えるには、*新しいテナントの管理リンク* をクリックします。

![新しいテナントの管理リンク](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> B2C テナントを運用アプリ向けに使用する予定がある場合は、 [運用スケールとプレビュー B2C テナントの比較](active-directory-b2c-reference-tenant-type.md)に関する記事を参照してください。 既存の B2C テナントを削除し、同じドメイン名を使用して再作成したときに発生する既知の問題があります。 B2C テナントは異なるドメイン名で作成する必要があります。
>
>

## <a name="link-your-tenant-to-your-subscription"></a>サブスクリプションへのテナントのリンク

すべての B2C 機能を有効にして使用料を支払うには、Azure AD B2C テナントを Azure サブスクリプションにリンクする必要があります。 詳しくは、[こちらの記事](active-directory-b2c-how-to-enable-billing.md)をご覧ください。 Azure AD B2C テナントを Azure サブスクリプションにリンクしていない場合は、一部の機能がブロックされ、B2C 設定に警告メッセージ ("この B2C テナントにリンクされたサブスクリプションがありません。サブスクリプションを確認してください。") が表示されます。 アプリを運用環境に移行する前に、この手順を実行することが重要です。

## <a name="easy-access-to-settings"></a>設定への簡単なアクセス

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

ポータル上部にある **[リソースの検索]** に `Azure AD B2C` を入力してブレードにアクセスすることもできます。 結果リストで **[Azure AD B2C]** を選択して [B2C setting]\(B2C 設定\) ブレードにアクセスします。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [B2C テナントでの B2C アプリケーションの登録](active-directory-b2c-app-registration.md)
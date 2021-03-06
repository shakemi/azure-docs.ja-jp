---
title: "Azure Active Directory B2B コラボレーションの招待の委任 | Microsoft Docs"
description: "Azure Active Directory B2B コラボレーション ユーザーのプロパティは構成できます"
services: active-directory
documentationcenter: 
author: twooley
manager: mtillman
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: twooley
ms.reviewer: sasubram
ms.openlocfilehash: facf0f62823c84742986c9fb585990d7fedb2ab1
ms.sourcegitcommit: 782d5955e1bec50a17d9366a8e2bf583559dca9e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2018
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Azure Active Directory B2B コラボレーションの招待の委任

Azure Active Directory (Azure AD) 企業間 (B2B) コラボレーションでは、グローバル管理者でなくても招待を送信できます。 それには、ポリシーを使用して、招待の送信が許可されているロールを持つユーザーに招待を委任します。 ゲスト ユーザーの招待を委任するための重要な新しい方法は、ゲストの招待元ロールを通じた方法です。

## <a name="guest-inviter-role"></a>ゲストの招待元ロール
ゲストの招待元ロールにユーザーを割り当てて、招待を送信することができます。 全体管理者ロールのメンバーである必要はありません。 既定では、全体管理者が通常のユーザーの招待を無効にしていない限り、通常のユーザーも招待 API を呼び出すことができます。 ユーザーは、Azure ポータルまたは PowerShell を使用して API を呼び出すこともできます。

次の例は、PowerShell を使って、ゲストの招待元ロールにユーザーを追加する方法を示しています。

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>招待できるユーザーの制御

![招待する方法を制御する](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Azure AD B2B コラボレーションでは、テナント管理者が次の招待ポリシーを設定できます。

- 招待を無効にする
- 管理者と、ゲストの招待元ロールのユーザーのみが招待できる
- 管理者、ゲストの招待元ロール、およびメンバーが招待できる
- ゲストを含むすべてのユーザーが招待できる

既定では、テナントは #4  (ゲストを含むすべてのユーザーが B2B ユーザーを招待できる) に設定されます。

## <a name="next-steps"></a>次の手順

Azure AD B2B コラボレーションに関する他の記事を参照してください。

* [Azure AD B2B コラボレーションとは](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B コラボレーション ユーザーのプロパティ](active-directory-b2b-user-properties.md)
* [B2B コラボレーション ユーザーのロールへの追加](active-directory-b2b-add-guest-to-role.md)
* [動的グループと B2B コラボレーション](active-directory-b2b-dynamic-groups.md)
* [B2B コラボレーション コードと PowerShell サンプル](active-directory-b2b-code-samples.md)
* [B2B コラボレーション用の SaaS アプリの構成](active-directory-b2b-configure-saas-apps.md)
* [B2B コラボレーション ユーザーのトークン](active-directory-b2b-user-token.md)
* [B2B コラボレーション ユーザーの要求マッピング](active-directory-b2b-claims-mapping.md)
* [Office 365 の外部共有](active-directory-b2b-o365-external-user.md)
* [B2B コラボレーションの現在の制限](active-directory-b2b-current-limitations.md)

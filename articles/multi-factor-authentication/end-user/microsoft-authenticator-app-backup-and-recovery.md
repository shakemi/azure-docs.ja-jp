---
title: Microsoft Authenticator を使用した情報のバックアップと復旧- Azure | Microsoft Docs
description: Microsoft Authenticator アプリを使用してアカウント資格情報をバックアップおよび復旧する方法を説明します。
services: multi-factor-authentication
documentationcenter: ''
author: eross-msft
manager: mtillman
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2018
ms.author: lizross
ms.reviewer: olhaun
ms.custom: end-user
ms.openlocfilehash: 0b76d2debb9814188e5551252e52bd0dae38eb50
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="backup-and-recover-account-credentials-with-the-microsoft-authenticator-app"></a>Microsoft Authenticator アプリを使用してアカウント資格情報をバックアップおよび復旧する
**適用対象:**

- iOS デバイス

Microsoft Authenticator アプリは、アカウント資格情報と、アカウントの順序などの関連アプリ設定をクラウドにバックアップします。 バックアップ後に、アプリを使用して情報を新しいデバイスに復旧することもできます。これにより、ロックアウトやアカウントの再作成の必要性を回避できる可能性があります。

>[!IMPORTANT]
> バックアップの保存場所ごとに 1 つの個人用 Microsoft アカウントと 1 つの iCloud アカウントが必要です。 ただし、その保存場所内で複数のアカウントをバックアップできます。 たとえば、個人用アカウント、学校のアカウントと、Facebook や Google などのサードパーティのアカウントがある場合があります。<br><br>アカウント資格情報のみが格納され、これにはユーザー名と 8 桁のアカウント確認コードが含まれます。この確認コードは、Microsoft Authenticator アプリを使用して本人確認を行うために必要です。 電子メールやファイルなど、アカウントに関連付けられているその他の情報は格納されません。 アカウントをなんらかの方法で他の製品やサービスに関連付けたり共有したりすることはありません。 最後に、IT 管理者がこれらのアカウントに関する情報を取得することはありません。

## <a name="back-up-your-account-credentials"></a>アカウントの資格情報のバックアップ
資格情報をバックアップする前に、次の両方が必要です。

- 復旧アカウントとして機能する個人用 [Microsoft アカウント](https://account.microsoft.com/account)。

- 実際の保存場所となる [iCloud アカウント](https://www.icloud.com/)。 

両方のアカウントへのサインインを要求すると、バックアップ情報のセキュリティが向上します。

**クラウド バックアップを有効にするには**
-   iOS デバイスで、**[設定]**、**[バックアップ]** の順に選択し、**[自動バックアップ]** をオンにします。

    アカウントの資格情報は、自分の iCloud アカウントにバックアップされます。

    ![自動バックアップ設定の場所を表示している iOS の設定画面](./media/authenticator-app-backup-and-recovery/backup-and-recovery-turn-on.png)

## <a name="recover-your-account-credentials-on-your-new-device"></a>アカウント資格情報を新しいデバイスに復旧する
情報をバックアップしたときに設定したのと同じ Microsoft 復旧アカウントを使用して、アカウント資格情報を iCloud アカウントから復旧できます。

**情報を復旧するには**
1.  iOS デバイスで、Microsoft Authenticator アプリを開き、画面の下部から **[回復の開始]** を選択します。

    ![[回復の開始] をクリックする場所を示している Microsoft Authenticator アプリ](./media/authenticator-app-backup-and-recovery/backup-and-recovery-begin-recovery.png)

2.  バックアップ プロセス中に使用したのと同じ個人用 Microsoft アカウントを使用して、復旧アカウントにサインインします。

    アカウント資格情報が新しいデバイスに復旧されます。

復旧が完了すると、Microsoft Authenticator アプリで個人用 Microsoft アカウントの検証コードが新旧の携帯電話間で異なることに気付く可能性があります。 各デバイスに独自の一意の資格情報があるためコードが異なりますが、どちらも有効で、関連付けられている携帯電話を使用してサインインするときに機能します。

## <a name="recover-additional-accounts-requiring-more-verification"></a>さらに検証が必要な追加のアカウントを復旧する
個人用アカウント、職場アカウント、または学校アカウントでプッシュ通知を使用する場合、情報を復旧する前に追加の検証を提供する必要があることを示すアラートが画面に表示されます。 プッシュ通知では、ネットワーク経由で送信されることのない、特定のデバイスに関連付けられた資格情報を使用する必要があるので、デバイスで資格情報を作成する前に本人確認が必要です。

個人用 Microsoft アカウントの場合、代替電子メールや電話番号と共にパスワードを入力して本人確認することができます。 職場または学校アカウントの場合は、アカウント プロバイダーから提供された QR コードをスキャンする必要があります。

**個人用アカウントに対して追加の検証を提供するには**
1.  Microsoft Authenticator アプリの **[アカウント]** 画面で、復旧するアカウントの横にあるドロップダウン矢印を選択します。

    ![使用可能なアカウントとそれに関連付けられたドロップダウン矢印を表示している Microsoft Authenticator アプリ](./media/authenticator-app-backup-and-recovery/backup-and-recovery-arrow.png)

2.  **[Sign in to recover]\(サインインして復旧する\)** を選択し、追加の検証として電子メール アドレスまたは電話番号を確認します。

    ![サインイン情報を入力できる Microsoft Authenticator アプリ](./media/authenticator-app-backup-and-recovery/backup-and-recovery-sign-in.png)

**職場または学校アカウントに対して追加の検証を提供するには**
1.  Microsoft Authenticator アプリの **[アカウント]** 画面で、復旧するアカウントの横にあるドロップダウン矢印を選択します。

    ![使用可能なアカウントとそれに関連付けられたドロップダウン矢印を表示している Microsoft Authenticator アプリ](./media/authenticator-app-backup-and-recovery/backup-and-recovery-additonal-accts.png)

2.  **[Scan QR code to recover]\(QR コードをスキャンして復旧\)** を選択し、管理者によって提供される QR コードをスキャンします。

    ![QR コードをスキャンできる Microsoft Authenticator アプリ](./media/authenticator-app-backup-and-recovery/backup-and-recovery-scan-qr-code.png)

## <a name="troubleshooting-backup-and-recovery-problems"></a>バックアップと復旧に関する問題のトラブルシューティング
バックアップを使用できない理由はいくつかあります。

-   **オペレーティング システムの変更。** バックアップは、携帯電話のオペレーティング システムによって提供されるクラウド ストレージ オプションに保存されるので、Android と iOS の間を切り替えるとバックアップを使用できません。 このような状況では、アプリ内にアカウントを手動で再作成する必要があります。

-   **ネットワークまたはパスワードの問題。** ネットワークに接続し、前回 iPhone で使用したのと同じ AppleId を使用して iCloud アカウントにサインインしていることを確認します。

-   **不注意による削除。** 以前のデバイスから、またはクラウド ストレージ アカウントの管理中にバックアップ アカウントを削除した可能性があります。 このような状況では、アプリ内にアカウントを手動で再作成する必要があります。

-   **既存の Microsoft Authenticator アカウント。** Microsoft Authenticator アプリ内にアカウントを既に設定してある場合、アプリではバックアップしたアカウントを復旧できません。 復旧防止により、アカウントの詳細情報が古い情報で上書きされないことが保証されます。 このような状況では、バックアップを復旧する前に Authenticator アプリで設定した既存のアカウントから既存のアカウント情報を削除する必要があります。

## <a name="next-steps"></a>次の手順
アカウントの資格情報をバックアップし、新しいデバイスに復旧したので、Microsoft Authenticator アプリを使用した本人確認に進むことができます。

## <a name="related-topics"></a>関連トピック
- [Microsoft Authenticator アプリの概要](microsoft-authenticator-app-how-to.md)  

- [携帯電話を使用したサインイン](microsoft-authenticator-app-phone-signin-faq.md)

- [Microsoft Authenticator アプリに関する FAQ](microsoft-authenticator-app-faq.md)

- [Multi-factor Authentication](https://docs.microsoft.com/en-us/azure/multi-factor-authentication/)
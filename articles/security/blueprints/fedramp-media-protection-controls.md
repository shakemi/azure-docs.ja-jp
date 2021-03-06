---
title: "Azure のセキュリティとコンプライアンスのブループリント - FedRAMP Web アプリケーションの自動化 - メディア保護"
description: "FedRAMP Web アプリケーションの自動化 - メディア保護"
services: security
documentationcenter: na
author: jomolesk
manager: mbaldwin
editor: tomsh
ms.assetid: fe86fd92-ef6b-4d17-a4a2-de6796d251d0
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/08/2018
ms.author: jomolesk
ms.openlocfilehash: 37812c2f7ee79685f9014a7999b4355e649ca6e1
ms.sourcegitcommit: 4723859f545bccc38a515192cf86dcf7ba0c0a67
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2018
---
# <a name="media-protection-mp"></a>メディア保護 (MP)

> [!NOTE]
> この管理策は、NIST および米国商務省により、NIST Special Publication 800-53 Revision 4 の一部として定義されています。 各コントロールのテスト手順およびガイダンスについては、NIST 800-53 Rev. 4 を参照してください。

## <a name="nist-800-53-control-mp-1"></a>NIST 800-53 コントロール MP-1

#### <a name="media-protection-policy-and-procedures"></a>メディア保護のポリシーと手順

**PL-1** 組織は、目的、範囲、役割、責任、経営陣のコミットメント、組織エンティティ間の調整、およびコンプライアンスを取り上げたメディア保護ポリシーと、メディア保護ポリシーおよびメディア保護の関連する管理策の実装を容易にする手順を策定、文書化し、[割り当て: 組織が定義した担当者または役割]に周知徹底する。また、現在のメディア保護ポリシーを[割り当て: 組織が定義した頻度]、メディア保護の手順を[割り当て: 組織が定義した頻度]で見直し、更新する。

**責任:** `Customer Only`

|||
|---|---|
| **お客様** | 顧客のエンタープライズ レベルのメディア保護のポリシーと手順で、この管理策に対処できます。 |
| **プロバイダー (Microsoft Azure)** | 適用外 |


 ## <a name="nist-800-53-control-mp-2"></a>NIST 800-53 コントロール MP-2

#### <a name="media-access"></a>メディア アクセス

**MP-2** 組織は、[割り当て: 組織が定義したデジタル/デジタルでないメディアのタイプ]へのアクセスを[割り当て: 組織が定義した職員または役割]に制限する。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、Microsoft セキュリティ ポリシーの実装によってメディア アクセスを実装しています。 デジタル メディアへの論理的なアクセスは、Active Directory グループ ポリシー オブジェクト (AD GPO) とセキュリティ グループによって制御されます。 すべてのメディアへの物理的なアクセスは、データセンター アクセス手順によって制限されます。 アクセスは、データにアクセスするための合法的なビジネス上の目的を持つ個人に制限されます。 適切なデータセンターのアクセス制御の詳細については、PE-3、物理的なアクセスの制御を参照してください。 Asset Protection Standard は、Microsoft Azure データセンター内の情報資産の機密性、完全性、および利用可能性を保護するために必要な保護を定義しています。 |


 ## <a name="nist-800-53-control-mp-3a"></a>NIST 800-53 コントロール MP-3.a

#### <a name="media-marking"></a>メディアのマーキング

**MP-3.a** 組織は、情報システムのメディアに、配布制限、取り扱いに関する警告、および適用されるセキュリティのマーキング (存在する場合) を示すマークを付ける。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、Microsoft データセンター内の資産に、さまざまなレベルのセキュリティおよび取り扱い上の注意に必要な HBI、MBI、または LBI (高、中、低のビジネスに対する影響) の指定のマークを付けます。 資産の所有者は、Microsoft データセンターに保管されている自身の資産を分類することが要求されます。 詳細については、Asset Classification Standard および Asset Protection Standard を参照してください。 |


 ## <a name="nist-800-53-control-mp-3b"></a>NIST 800-53 コントロール MP-3.b

#### <a name="media-marking"></a>メディアのマーキング

**MP-3.b** 組織は、メディアが[割り当て: 組織が定義した制御対象エリア]内に保管されている場合に限り、[割り当て: 組織が定義した情報システムのメディア タイプ]をマーキングの対象外とする。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は資産所有者にその資産に資産区分を割り当てることを要求し、この要件を免除される資産はありません。 Microsoft データセンター環境では、資産とはサーバー、ネットワーク デバイス、および磁気テープを指します。 USB フラッシュ/サム ドライブ、外部/リムーバブル ハードディスク ドライブ、CD/DVD などのその他のデジタル メディアは使用されません。 デジタルでないメディアは、データセンターでは使用されません。 |


 ## <a name="nist-800-53-control-mp-4a"></a>NIST 800-53 コントロール MP-4.a

#### <a name="media-storage"></a>メディアの保管

**MP-4.a** 組織は、[割り当て: 組織が定義した制御対象エリア]の[割り当て: 組織が定義したデジタル/デジタル以外のメディアのタイプ]を物理的に制御し、安全に保管する。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure のデジタル メディア資産は、データセンターのコロケーション ルーム内に物理的かつ安全に保管されます。 Microsoft データセンターには安全に保管するための、複数の層の物理的なアクセスの制御 (アクセス バッジ、生体認証。物理的なアクセスの制御の詳細については、PE-3 を参照) および適所の監視カメラがあります。 デジタル メディアには、サーバー、ネットワーク デバイス、およびバックアップ用に使用される磁気テープがあります。 デジタルでないメディアは、データセンター環境では使用されません。 |


 ## <a name="nist-800-53-control-mp-4b"></a>NIST 800-53 コントロール MP-4.b

#### <a name="media-storage"></a>メディアの保管

**MP-4.b** 組織は、承認済みの機器、技術、および手順を使用してメディアが破壊またはサニタイズされるまで、情報システムのメディアを保護する。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure のデジタル メディア資産は、資産の有効期間に対する物理的なアクセスの制御 (PE-3) および論的なアクセスの制御 (IA-2) によって、Microsoft データセンターのコロケーションで保護されます。 Microsoft Azure の資産は、資産の破棄の前に NIST SP 800-88 に合致する方法でクリア、消去、または破棄されます。 資産の破壊の場合、Microsoft Azure はオンサイトの資産破壊サービスを利用します。 |


 ## <a name="nist-800-53-control-mp-5a"></a>NIST 800-53 コントロール MP-5.a

#### <a name="media-transport"></a>メディアの輸送

**MP-5.a** 組織は、 [割り当て: 組織が定義したセキュリティ保護]を使用した制御対象エリア外への輸送中、[割り当て: 組織が定義した情報システムのメディア タイプ]を保護し、制御する。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft データセンターにある Microsoft Azureにデジタル メディアは、必要に応じてサーバー、ネットワーク デバイス、磁気バックアップ テープおよびディスクで構成されます。 Microsoft データセンターではデジタルでないメディアは使用されません。 Microsoft では、データセンターの外部に輸送されるメディアを保護するために、1) 安全な輸送、2) 暗号化、3) クレンジング、消去、または破棄という 3 つの方法を使用します。 |


 ## <a name="nist-800-53-control-mp-5b"></a>NIST 800-53 コントロール MP-5.b

#### <a name="media-transport"></a>メディアの輸送

**MP-5.b** 組織は、制御対象エリア外への輸送中、情報システムのメディアについての説明責任を保持する。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、NIST SP 800-88 (一貫性のあるクレンジング/消去、資産の破棄、暗号化、正確なインベントリ作成、追跡、および輸送中の生産物流管理の保護) のガイダンスによって、資産がデータセンターから離れることについての説明責任を保持します。 |


 ## <a name="nist-800-53-control-mp-5c"></a>NIST 800-53 コントロール MP-5.c

#### <a name="media-transport"></a>メディアの輸送

**MP-5.c** 組織は、情報システムのメディアの輸送に関連する活動を文書化する。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、輸送前のインベントリ、輸送中の生産物流管理の追跡および保護、輸送後の資産のクレンジング/消去、資産の破壊、資産の受領、およびインベントリの確認の記録を保持します。 |


 ## <a name="nist-800-53-control-mp-5d"></a>NIST 800-53 コントロール MP-5.d

#### <a name="media-transport"></a>メディアの輸送

**MP-5.d** 組織は、情報システムのメディアの輸送に関連する活動を、権限を与えられた職員に限定する。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、生産物流管理の保護によって、資産の輸送活動を、権限を与えられた職員に限定します。 資産インベントリの施錠、改ざん防止シール、必要な確認の利用によって、資産の輸送時に権限のある職員のみが関与することが保証されます。 |


 ### <a name="nist-800-53-control-mp-5-4"></a>NIST 800-53 コントロール MP-5 (4)

#### <a name="media-transport--cryptographic-protection"></a>メディアの輸送 | 暗号化による保護

**MP-5 (4)** 情報システムは、制御対象エリア外への輸送中、デジタル メディアに保管されている情報の機密性と整合性を保護する暗号化メカニズムを実装します。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、磁気テープ上の AES 256 ビットの暗号化されたデータを保護するために、FIPS 140-2 レベル 3 で有効な暗号化モジュール (cert #1694) および HSM (cert #1178) を使用して暗号化キーを管理する、データ保護サービス (DPS) を採用しています。 |


 ## <a name="nist-800-53-control-mp-6a"></a>NIST 800-53 コントロール MP-6.a

#### <a name="media-sanitization"></a>メディアのサニタイズ

**MP-6.a** 組織は、適用される連邦および組織の標準とポリシーに従って、[割り当て: 組織が定義したサニタイズの手法と手順]を使用した廃棄、組織の管理外への放棄、再利用のための放棄の前に、[組織が定義した情報システムのメディア]をサニタイズする。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、再利用または廃棄の前に、Microsoft Azure 認定ツールを使用して、かつ、NIST SP 800-88、メディアのサニタイズのガイドラインに準拠する方法で、Microsoft Azure データセンター環境にあるデジタル メディアをクレンジング/消去することを要求します。 デジタルでないメディアは、データセンター環境の Microsoft Azure では使用されません。 |


 ## <a name="nist-800-53-control-mp-6b"></a>NIST 800-53 コントロール MP-6.b

#### <a name="media-sanitization"></a>メディアのサニタイズ

**MP-6.b** 組織は、情報のセキュリティのカテゴリまたは区分に応じた強度と整合性を備えたサニタイズ メカニズムを採用する。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、データ消去ユニットおよびプロセスを使用して、NIST SP 800-88、および資産に関する Microsoft Azure の資産区分に応じた方法で、データをクレンジング/消去します。 破壊が必要な資産の場合、Microsoft Azure はオンサイトの資産破壊サービスを利用します。 |


 ### <a name="nist-800-53-control-mp-6-1"></a>NIST 800-53 コントロール MP-6 (1)

#### <a name="media-sanitization--review--approve--track--document--verify"></a>メディアのサニタイズ | レビュー / 承認 / 追跡 / 文書化 / 検証

**MP-6 (1)** 組織は、メディアのサニタイズおよび廃棄活動をレビュー、承認、追跡、文書化、および検証します。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure には、Asset Classification Standard および Asset Protection Standard についての NIST SP 800-88 のガイダンスに従ったメディアのサニタイズ手順が実装されています。 すべての磁気または電子メディアは、その Azure 資産区分に従って NIST SP 800-88 仕様に従うことでクレンジング/消去されます。 Azure は、Extreme Protocol Solutions (EPS) のデータ消去ユニットを利用しています。 EPS ソフトウェアは、クレンジングおよび消去/安全な消去についての NIST SP 800-88 要件に対応しています。 |


 ### <a name="nist-800-53-control-mp-6-2"></a>NIST 800-53 コントロール MP-6 (2)

#### <a name="media-sanitization--equipment-testing"></a>メディアのサニタイズ | 機器のテスト

**MP-6 (2)** 組織は、意図したサニタイズが達成されたことを確認するため、[割り当て: 組織が定義した頻度]でサニタイズの機器と手順をテストする。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、データ消去ユニットおよびプロセスを使用して、NIST SP 800-88 に合致する方法でデータをクレンジング/消去します。 180 日ごとに DCS オペレーションが Microsoft Azure のデータ消去ユニットと消去のプロセスをテストします。 このテストで DCS オペレーションは、テストされたハードディスク ドライブの法医学的分析によって意図したサニタイズが達成されていることを確認することで、データがデータ消去ユニットによってサニタイズされたことを確認します。 |


 ### <a name="nist-800-53-control-mp-6-3"></a>NIST 800-53 コントロール MP-6 (3)

#### <a name="media-sanitization--nondestructive-techniques"></a>メディアのサニタイズ | 非破壊法

**MP-6 (3)** 組織は、 次の状況下では、ポータブル ストレージ デバイスを情報システムに接続する前に、当該デバイスに非破壊サニタイズ法を適用する: [割り当て: ポータブル ストレージ デバイスのサニタイズを必要とする、組織が定義した状況]。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は、ポータブル ストレージ デバイス上のマルウェアによって政府機関の環境が感染することを防ぐために、Azure データセンターがデータセンター サービス ランブックのツールおよびリムーバブル メディアのセキュリティ手順に確実に従うようにします。 この手順は、USB ドライブを政府機関の環境で使用する前に、次の処置を取ることを指定しています。 <br /> (1) ドライブを製造元またはベンダーから初めて購入したとき、最初の使用の前、または別のツール用に再利用するときは、USB ドライブをフォーマットする。 <br /> (2) USB ドライブを政府機関の指定エリアに持ち込む前に、エリア内で使用するドライブのマルウェアをスキャンする。 <br /> (3) 政府機関の指定エリア内でドライブを使用した後、エリアから出す前にドライブをフォーマットする。 <br /> ツールおよびリムーバブル メディアのセキュリティ手順では、紛失、破棄、盗難、または紛れ込んだサム ドライブが Azure データセンターに再度入り込むことがないようにしながらも、それらをカタログ化し、破棄することを要求しています。 |


 ## <a name="nist-800-53-control-mp-7"></a>NIST 800-53 コントロール MP-7

#### <a name="media-use"></a>メディアの使用

**MP-7** 組織は、 [割り当て: 組織が定義したセキュリティ保護]を使用して、[割り当て: 組織が定義した情報システムまたはシステム コンポーネント]上の[割り当て: 組織が定義した情報システムのメディア タイプ]を[選択項目: 制限; 禁止]する。

**責任:** `Azure Only`

|||
|---|---|
| **お客様** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft Azure は資産所有者に、その資産に資産区分を割り当てることを要求し、この要件を免除される資産はありません。 Microsoft Azure データセンター環境では、資産とはサーバー、およびネットワーク デバイスを指します。 USB フラッシュ/サム ドライブなどのその他のデジタル メディアは、それらのデバイスの管理方法に影響する特定のポリシーと手順によって管理されます。 CD/DVD は使用されません。 デジタルでないメディアは、データセンターでは使用されません。 Microsoft Azure データセンター環境でのデジタル メディアの使用は、CCTV 受信地域を介して 24 時間 365 日監視されます。 詳細については、PE-06 を参照してください。 |


 ### <a name="nist-800-53-control-mp-7-1"></a>NIST 800-53 コントロール MP-7 (1)

#### <a name="media-use--prohibit-use-without-owner"></a>メディアの使用 | 所有者なしでの使用の禁止

**MP-7 (1)** 組織は、ポータブル ストレージ デバイスの所有者を確認できない場合は、組織の情報システムで当該デバイスを使用することを禁ずる。

**責任:** `Azure Only`

|||
|---|---|
| **顧客** | Azure 上にデプロイされたシステムの範囲内には、顧客が制御するメディアはありません。 |
| **プロバイダー (Microsoft Azure)** | Microsoft では、書き込み可能なリムーバブル メディアの使用を、DCS ツールおよびリムーバブル メディア手順によるデータセンター管理で明示的に承認されているメディアに制限しています。 Microsoft データセンター就業規則に記載の通り、個人で所有しているメディア、または所有者を特定できないメディアは、すべての生産エリアで禁止されています。 |

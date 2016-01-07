---
description: na
keywords: na
pagetitle: Rights Management sharing application: Version release history
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
---
# Rights Management 共有アプリケーション: バージョン リリース履歴
Rights Management チームは、Rights Management 共有アプリケーションの修正プログラムと新機能を定期的に更新しています。 次の情報を使用して、リリースの新機能や変更内容をご確認ください。 最新のリリースは一番上に表示されます。

2015 年 1 月 1 日より前のバージョンは表示されません。

> [!NOTE]
> RMS 共有アプリケーションに関するフィードバックまたはご質問については、[AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question) まで電子メール メッセージをお送りください。

## バージョン 1.0.2004.0
**リリース日**:2015/12/11

**修正内容**:

-   エラー メッセージの改善 (正確さと明確さ)。

-   コンテンツの暗号化と暗号化解除に関するパフォーマンスの向上。

**新機能**:

-   管理者以外によるインストールのサポート。これにより、標準ユーザーは RMS 共有アプリケーションをインストールできます。

    Office 2010 を実行している標準ユーザーの場合は、いくつか制限があります。 詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](../Topic/Download_and_install_the_Rights_Management_sharing_application.md)」の「[ローカル管理者ではなく、かつ Office 2010 を使用している場合](../Topic/Download_and_install_the_Rights_Management_sharing_application.md#BKMK_SetupOffice2010)」セクションにあるユーザー用の手順を参照してください。

## バージョン 1.0.1908.0
**リリース日**:9/16/2015

**修正内容**:

-   Azure RMS 用の多要素認証 (MFA) をサポートするようになりました。それにより、最新の認証を利用するアプリケーションの Microsoft サインイン アシスタントへの依存関係が削除されました。

    詳細については、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」の[多要素認証 (MFA) と Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_MFA)セクションをご覧ください。

## バージョン 1.0.1784.0
**リリース日**:7/30/2015

**修正内容**:

-   権限ポリシー テンプレートの既定の更新間隔が 7 日から 1 日に短縮されました。

-   少数の回帰とマイナー バグ。

## バージョン 1.0.1770.0
**リリース日**:4/25/2015

**修正内容**:

-   所有者と共同所有者のみが保護を削除できるようになりました。 共同作成者は保護を削除できません。

-   ネットワーク共有上のファイルを保護できるようになりました。

**新機能**:

-   ドキュメントの追跡と取り消しをサポートします。 詳細については、「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](../Topic/Track_and_revoke_your_documents_when_you_use_the_RMS_sharing_application.md)」を参照してください。

-   **[保護ファイルの共有]** を選んだ場合のテンプレートのサポート:

    -   テンプレートを選べるようになりました。

    -   スライダーの代わりに、テンプレートとカスタム アクセス許可を含むリスト ボックスが表示されます。

    -   **[すべてのデバイスで使用を許可する]** と **[使用制限を強制する]** のオプションが表示されなくなりました。 代わりに、ファイルの種類によって **[一般保護]** が自動的に選択されます。

    詳細については、「[Rights Management 共有アプリケーションのダイアログ ボックス オプション](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md)」を参照してください。

## バージョン 1.0.1667.0
**リリース日**:1/19/2015

**修正内容**:

-   RMS 共有アプリの PPDF ビューアーで中国語のフォントをサポートするようになりました。

-   エラー処理とメッセージングが向上しました。

-   新しいバージョンのアプリがダウンロード可能になったときの自動更新通知に関する問題が修正されました。

**新機能**:

-   **組織内の複数の電子メール ドメインのサポート**:AD RMS を使用している組織のユーザーが複数の電子メール ドメインを持つ場合、この更新プログラムによって、このユーザーは、他のドメイン内にある自分の組織のユーザーによって保護されているコンテンツを使用できます。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](../Topic/Rights_Management_sharing_application_administrator_guide.md)」の[AD RMS のみ: 組織内での複数の電子メール ドメインのサポート](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains)セクションをご覧ください。


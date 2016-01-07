---
description: na
keywords: na
pagetitle: Configuring Custom Templates for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
---
# Azure Rights Management のカスタム テンプレートを構成する
Azure Rights Management (Azure RMS) をアクティブ化した後で、ユーザーは 2 つの既定のテンプレートを自動的に使用できるようになります。これにより、組織内の承認されたユーザーにアクセスが制限されている機密ファイルにポリシーを簡単に適用できるようになります。 これらの 2 つのテンプレートには、次の権限ポリシーの制限があります。

-   保護されたコンテンツの読み取り専用の表示

    -   表示名: **&lt;組織名&gt; - 社外秘、表示のみ**

    -   特定の権限:コンテンツの表示

-   保護されたコンテンツの読み取りまたは変更の権限

    -   表示名: **&lt;組織名&gt; - 社外秘**

    -   特定の権限:コンテンツの表示、ファイルの保存、コンテンツの編集、割り当てられた権限の表示、Macro の許可、転送、返信、全員に返信

さらに、[RMS 共有アプリケーション](http://technet.microsoft.com/library/dn339006.aspx)を使用して、ユーザーが独自のアクセス許可のセットを定義することができます。 また、Outlook クライアントおよび Outlook Web Access の場合、ユーザーは電子メール メッセージの **[転送不可]** オプションを選択できます。

多くの組織では、既定のテンプレートで十分です。 ただし、独自のカスタム権限ポリシー テンプレートを作成する必要がある場合は、作成できます。 カスタム テンプレートを作成する理由として、次のようなケースが考えられます。

-   テンプレートですべてのユーザーではなく組織のユーザーのサブセットに権限を付与する必要がある。

-   組織のすべてのユーザーがアプリケーションのテンプレート (部門別テンプレート) を表示し、選択できるのではなく、一部のユーザーだけがそれを表示し、選択できるようにする必要がある。

-   表示と編集 (コピーと印刷を除く) などのテンプレートのカスタム権限を定義する必要がある。

-   有効期限や、インターネット接続なしでのコンテンツへのアクセスの可否などの追加のオプションをテンプレート内で構成する必要がある。

このような設定を含むカスタム テンプレートをユーザーが選択できるようにするには、最初にカスタム テンプレートを作成して構成してから発行する必要があります。

以下のセクションで、カスタム テンプレートの構成と使用について説明します。

-   [カスタム テンプレートを作成、構成、および発行する方法](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToConfigureCustomTemplates)

-   [テンプレートのコピー方法](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates)

-   [テンプレートを削除 (アーカイブ) する方法](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToArchiveTemplates)

-   [ユーザー用のテンプレートの更新](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates)

-   [Windows PowerShell リファレンス](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_PowerShellTemplates)

## <a name="BKMK_HowToConfigureCustomTemplates"></a>カスタム テンプレートを作成、構成、および発行する方法
カスタム テンプレートは、Azure クラシック ポータルで作成および管理します。 この作業は、Azure クラシック ポータルから直接行うことができます。また、Office 365 管理センターにサインインして、Rights Management の **[高度な機能]** を選択することもでき、これにより Azure クラシック ポータルにリダイレクトされます。

Rights Management のテンプレートを作成、構成、およびパブリッシュするには、次の手順を使用します。

#### カスタム テンプレートを作成するには

1.  Office 365 管理センターと Azure クラシック ポータルのどちらにサインインするかに応じて、次のいずれかを実行します。

    -   [Office 365 管理センター](https://portal.office.com/) から次の手順を実行します。

        1.  左ペインで、[**サービス設定**] をクリックします。

        2.  **[サービス設定]** ページで、**[Rights Management]** をクリックします。

        3.  [**情報を保護**] セクションで、[**管理**] をクリックします。

        4.  [**Rights Management**] セクションで、[**高度な機能**] をクリックします。

            > [!NOTE]
            > Rights Management をアクティブ化していない場合は、最初に [**アクティブ化**] をクリックして操作を確認します。 詳細については、「[Rights Management をアクティブにする](../Topic/Activating_Azure_Rights_Management.md)」を参照してください。
            > 
            > **[高度な機能]** をまだクリックしてない場合は、Rights Management をアクティブにした後、画面の指示に従って、Azure クラシック ポータルへのアクセスに必要な無料の Azure サブスクリプションを取得します。

            **[高度な機能]** をクリックすると、Azure クラシック ポータルが読み込まれ、ここで組織の Azure Active Directory の **[RIGHTS MANAGEMENT]** を管理できます。

    -   [Azure クラシック ポータル](http://go.microsoft.com/fwlink/p/?LinkID=275081)から、次の手順を実行します。

        1.  左ペインで、[**ACTIVE DIRECTORY**] をクリックします。

        2.  [**active directory**] ページで、[**RIGHTS MANAGEMENT**] をクリックします。

        3.  Rights Management で管理するディレクトリを選択します。

        4.  Rights Management をまだアクティブ化していない場合は、最初に **[アクティブ化]** をクリックして、操作を確認します。

            > [!NOTE]
            > 詳細については、「[Rights Management をアクティブにする](../Topic/Activating_Azure_Rights_Management.md)」を参照してください。

2.  新しいテンプレートの作成:

    -   Azure クラシック ポータルの **[Rights Management の使用を開始]** クイック スタート ページから、**[新しい権利ポリシー テンプレートを作成する]** をクリックします。

        Office 365 の指示に従った後に、このページがすぐに表示されない場合は、上記の Azure クラシック ポータルのナビゲーション手順を使用します。

3.  **[新しい権利ポリシー テンプレートの追加]** ページで、ユーザーに表示するテンプレート名と説明を入力する言語を選択します (後で言語を追加できます)。 次に、一意の名前と説明を入力し、[完了] ボタンをクリックします。

**[Rights Management の使用を開始]** クイック スタート ページから、**[権限ポリシー テンプレートの管理]** をクリックします。 新しく作成されたテンプレートがテンプレートの一覧に追加され、**[アーカイブ済み]** ステータスになっています。 この段階では、テンプレートは作成されていますが構成されていないため、ユーザーには表示されません。

#### カスタム テンプレートを構成および発行するには

1.  Azure クラシック ポータルの **[テンプレート]** ページから、新しく作成したテンプレートを選択します。

2.  **[テンプレートが追加されました]** クイック スタート ページで手順 1. の **[作業の開始]** をクリックし、**[ユーザーおよびグループの権限の構成]** をクリックして、**[今すぐ開始]** または **[追加]** をクリックし、新しいテンプレートによって保護されるコンテンツを使用する権限を持つユーザーおよびグループを選択します。

    > [!NOTE]
    > 選択するユーザーまたはグループは電子メール アドレスを持っている必要があります。 運用環境ではこの条件はほとんど常に満たされますが、単純なテスト環境では、ユーザー アカウントまたはグループへの電子メール アドレスの追加が必要になることがあります。

    ベスト プラクティスとして、ユーザーではなくグループを使用すると、テンプレートの管理が簡素化されます。 オンプレミスの Active Directory があり、Azure AD に同期している場合は、メールが有効なグループ (セキュリティ グループまたは配布グループ) を使用できます。 ただし、組織内のすべてのユーザーに権限を付与する場合は、複数のグループを指定するのでなく、既定のテンプレートのいずれか 1 つをコピーする方が効率的です。 詳細については、このトピックの「[テンプレートのコピー方法](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates)」セクションを参照してください。

    > [!TIP]
    > [Azure Rights Management 用 Windows PowerShell モジュール](https://technet.microsoft.com/library/jj585012.aspx)を使用し、次の方法のいずれかを使用して、後で組織の外部からテンプレートにユーザーを追加できます。
    > 
    > -   **権限定義オブジェクトを使用してテンプレートを更新する**:  権限定義オブジェクトで外部電子メール アドレスおよびその権限を指定し、これらを使用してテンプレートを更新します。[New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) コマンドレットを使用して権限定義オブジェクト指定し、変数を作成してから、[Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) コマンドレットを使用してこの変数を -RightsDefinition パラメーターに指定し、既存のテンプレートを変更します。 ただし、これらのユーザーを既存のテンプレートに追加する場合は、新しい外部ユーザーだけでなく、テンプレートに既存のグループの権限定義オブジェクトも定義する必要があります。
    > -   **更新されたテンプレートをエクスポート、編集、インポートする**： [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) コマンドレットを使用して、テンプレートをファイルにエクスポートします。このファイルを編集して、これらのユーザーの外部電子メール アドレスとその権限を既存のグループと権限に追加することができます。 その後 [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) コマンドレットを使用して、この変更を Azure RMS にインポートします。

3.  [次へ] ボタンをクリックし、表示されているいずれかの権限を選択したユーザーおよびグループに割り当てます。

    各権限の詳細 (とカスタム権限) については、表示されている説明を使用します。 詳細については、「[Azure Rights Management の使用権限を構成する](../Topic/Configuring_Usage_Rights_for_Azure_Rights_Management.md)」もご覧ください。 ただし、RMS をサポートするアプリケーションはこれらの権限の実装方法で異なる場合があります。 その文書を参照し、ユーザーが使用するアプリケーションで独自にテストし、動作を確認してからユーザーのテンプレートをデプロイします。 そのテストでこのテンプレートを管理者にのみ見せるには、このテンプレートを部門別テンプレートにします (手順 6)。

4.  **[カスタム]** を選択した場合は、[次へ] ボタンをクリックし、それらのカスタム権限を選択します。

    使用可能な個別の権限の任意の組み合わせを使用できますが、一部のアプリケーションでは、一部の権限が他の個別の権限に依存していることがあります。 この場合、依存する権限が自動的に選択されます。

    > [!TIP]
    > **[コンテンツのコピーと抽出]** 権限を追加することを検討し、この権限を選択した管理者か情報の復元に責任を持つ別の役割の担当者に付与します。 この権限を付与すると、必要な場合にこのテンプレートを使用して保護されるファイルやメールから保護が取り除かれます。 テンプレート レベルの保護を取り除くこの機能によって、スーパー ユーザー機能を使用するよりも詳細に制御できるようになります。

5.  [完了] ボタンをクリックします。

6.  アプリケーションでのテンプレートの一覧表示で特定のサブセットのユーザーのみに表示されるようにテンプレートを設定するには:**[スコープ]** をクリックし、これを部門別テンプレートとして設定し、**[今すぐ開始する]** をクリックします。 このように設定しない場合は、手順 9 に進みます。

    部門別テンプレートの追加情報:既定では、Azure ディレクトリのすべてのユーザーにすべての公開済みテンプレートが表示されます。コンテンツを保護するとき、アプリケーションから公開済みテンプレートを選択できます。 特定のユーザーにのみ一部の公開済みテンプレートを見せる場合、テンプレートのスコープを特定のユーザーに限定する必要があります。 その後、特定のユーザーのみがそのテンプレートを選択できます。 指定しない他のユーザーにはテンプレートが表示されず、選択できません。 この手法を利用すれば、より効率的に正しいテンプレートが選択されます。特定のグループまたは部門に使用してもらうようにテンプレートを作成するときに特に便利です。 ユーザーには自分に与えられたテンプレートのみが表示されます。

    たとえば、財務部門のメンバーに読み取り権限のみを適用するテンプレートを人事部門用に作成します。 人事部門のメンバーが Rights Management 共有アプリケーションを使用するとき、人事部門のメンバーだけがこのテンプレートを適用できます。「HumanResources」という名前の電子メール有効グループにテンプレートのスコープを限定すると、 そのグループのメンバーにのみこのテンプレートが表示され、メンバーはテンプレートを適用できます。

7.  **[テンプレートの表示]** ページで、RMS 対応アプリケーションのテンプレートを表示し、選択できるユーザーとグループを選択します。 前と同様に、ベスト プラクティスとしては、ユーザーではなくグループを利用します。選択したグループまたはユーザーには電子メール アドレスを与える必要があります。

8.  [次へ] ボタンをクリックし、部門別テンプレートのアプリケーション互換性を構成する必要があるかどうかを決定します。 必要がある場合、**[アプリケーションの互換性]** をクリックし、チェック ボックスを選択し、**[完了]** をクリックします。

    アプリケーションの互換性を構成する必要があるのはなぜでしょうか。 アプリケーションの一部では部門別テンプレートがサポートされません。 サポートするには、テンプレートをダウンロードする前に、アプリケーションは RMS サービスで認証する必要があります。 認証プロセスが行われない場合、既定では、部門別テンプレートはダウンロードされません。 この動作は上書きできます。その場合、すべての部門別テンプレートがダウンロードされるように指定し、アプリケーション互換性を構成し、**[アプリケーションでユーザー ID がサポートされていないときにこのテンプレートをすべてのユーザーに表示する]** チェックボックスを選択します。

    たとえば、人事部門の例で部門別テンプレートのアプリケーション互換性を構成しない場合、RMS 共有アプリケーションの使用時に人事部門のユーザーにのみ部門別テンプレートが表示されますが、Exchange Server 2013 の Outlook Web Access (OWA) の使用時にはどのユーザーにも部門別テンプレートは表示されません。Exchange OWA と Exchange ActiveSync は部門別テンプレートを現在サポートしていないためです。 アプリケーション互換性を構成し、この既定の動作を上書きする場合、RMS 共有アプリケーションの使用時に、人事部門のユーザーにのみ、部門別テンプレートが表示されるが、Outlook Web Access (OWA) の使用時は、すべてのユーザーに部門別テンプレートが表示されます。 ユーザーが Exchange Online の OWA または Exchange ActiveSync を使用する場合は、Exchange Online でのテンプレートの状態 (アーカイブまたは公開済み) に基づいて、すべてのユーザーに部門別テンプレートが表示されるか、どのユーザーにも部門別テンプレートは表示されません。

    Office 2016 では、部門別テンプレートがネイティブでサポートされます。最新の Office 更新プログラム ([KB 3054853](https://support.microsoft.com/kb/3054853)) が適用された Office 2013 でも、部門別テンプレートがネイティブでサポートされます。

    > [!NOTE]
    > アプリケーションがネイティブで部門別テンプレートをサポートしない場合、カスタム RMS テンプレート ダウンロード スクリプトまたは他のツールを利用し、これらのテンプレートをローカル RMS クライアント フォルダーにデプロイできます。 その後、テンプレート スコープで選択されたユーザーとグループにのみ、アプリケーションは部門別テンプレートを正しく表示します。
    > 
    > -   Office 2010 の場合は、クライアントのフォルダーは **%localappdata%\Microsoft\DRM\Templates** になります。
    > -   すべてのテンプレートをダウンロードしたクライアント コンピューターから、テンプレート ファイルをコピーし、他のコンピューターに貼り付けることができます。
    > 
    > [Microsoft Connect サイトからカスタム RMS テンプレート スクリプトをダウンロードする](http://go.microsoft.com/fwlink/?LinkId=524506)ことができます。 このリンクをクリックしたときにエラーが表示される場合は、Microsoft Connect への登録が完了していない可能性があります。   登録するには、次の手順を実行します。
    > 
    > 1.  [Microsoft Connect サイト](http://www.connect.microsoft.com)に移動し、Microsoft アカウントでサインインします。
    > 2.  **[ディレクトリ]** をクリックし、**[現在フィードバック対象外の製品を Connect で表示]** カテゴリを選択します。
    > 3.  **Rights Management Services** と **Microsoft RMS Enterprise Features** プログラムを探して、**[参加]** をクリックします。

9. **[構成]** をクリックし、ユーザーが使用する言語を追加し、さらにこのテンプレートの名前と説明をその言語で追加します。 複数言語に対応する場合は、ユーザーが使用する各言語を追加し、その言語で名前と説明を入力することが重要です。 これにより、ユーザーはクライアント オペレーティング システムと同じ言語でテンプレートの名前と説明を表示できるので、ドキュメントや電子メール メッセージに適用されるポリシーを確実に理解することができます。 ユーザーのクライアント オペレーティング システムと一致する言語がない場合、ユーザーに表示される言語と説明は、テンプレートを最初に作成したときに定義した言語と説明に戻ります。

    次に、次の設定を変更するかどうかを確認します。

    |設定|詳細情報|
    |------|--------|
    |**[コンテンツの有効期限]**|このテンプレートによって保護されているファイルを開けなくなる日付またはそれまでの日数を定義します。 日付を指定するか、保護がファイルに適用された時点からの日数を指定することができます。<br /><br />日付を指定する場合は、現在のタイム ゾーンの午前 0 時から有効になります。|
    |**[オフライン アクセス]**|この設定を使用して、ユーザーがインターネットに接続されていないときに保護されたファイルを開ける必要がある要件に対して、セキュリティ要件のバランスを取ります。<br /><br />インターネットに接続されていないときにコンテンツを使用できないように指定するか、コンテンツが指定された日数のみ利用できるように指定した場合、そのしきい値に達すると、ユーザーは再認証される必要があり、アクセスがログに記録されます。 この場合、ユーザーの資格情報がキャッシュされていない場合、ユーザーはファイルを開く前にサインインするように要求されます。<br /><br />再認証に加えて、ポリシーおよびユーザー グループのメンバーシップが再評価されます。 つまり、ユーザーが最後にファイルにアクセスした後にポリシーまたはグループ メンバーシップが変更された場合、ユーザーが同じファイルにアクセスしたときに異なる結果になる可能性があります。|

10. ユーザー用のテンプレートが適切に構成されていると確信できる場合は、**[発行]** をクリックして、テンプレートがユーザーに表示されるようにし、**[保存]** をクリックします。

11. クラシック ポータルの [戻る] ボタンをクリックして、**[テンプレート]** ページに戻ると、テンプレートのステータスが **[発行済み]** に更新されています。

テンプレートを変更するには、テンプレートを選択し、クイック スタート手順をもう一度使用します。 または、次のいずれかのオプションを選択します。

-   ユーザーおよびグループを追加してそれらのユーザーおよびグループの権限を定義するには:[**権限**] をクリックし、[**追加**] をクリックします。

-   以前に選択したユーザーまたはグループを削除するには:**[権限]** をクリックし、一覧からユーザーまたはグループを選択して、**[削除]** をクリックします。

-   アプリケーションから選択するテンプレートを表示できるユーザーを変更するには:**[スコープ]** をクリックし、**[追加]** または **[削除]** または **[アプリケーションの互換性]** をクリックします。

-   テンプレートがすべてのユーザーに表示されないようにするには:**[構成]** をクリックし、**[アーカイブ]** をクリックして、**[保存]** をクリックします。

-   他の構成を変更するには:**[構成]** をクリックし、変更を加えて、**[保存]** をクリックします。

> [!WARNING]
> 以前に保存したテンプレートを変更した場合、クライアントのコンピューターでテンプレートが更新されるまで、クライアントにはそれらのテンプレートの変更が表示されません。 詳細については、このトピックの「[ユーザー用のテンプレートの更新](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates)」セクションを参照してください。

## <a name="BKMK_HowToCopyTemplates"></a>テンプレートのコピー方法
既存のテンプレートとよく似た設定の新しいテンプレートを作成する場合、**[テンプレート]** ページで元のテンプレートを選択し、**[コピー]** をクリックして、一意の名前を指定し、必要な変更を加えます。

> [!IMPORTANT]
> テンプレートをコピーすると、**[発行済み]** または **[アーカイブ済み]** のステータスもコピーされます。 発行済みのテンプレートをコピーする場合、ステータスを変更しない限り直前の状態は発行済みになります。

カスタム テンプレートと既定のテンプレートをコピーすることができます。 ベスト プラクティスとして、テンプレートによって組織内のすべてのユーザーに権限を付与する場合に、新しいカスタム テンプレートを作成するのでなく、既定のテンプレートのいずれか 1 つをコピーします。 この方法を利用すれば、すべてのユーザーを指定する場合に複数のグループを作成または選択する必要がなくなります。 ただし、このシナリオでは、追加の言語に対応するためにコピーされるテンプレートについては新しい名前と説明を必ず指定します。

## <a name="BKMK_HowToArchiveTemplates"></a>テンプレートを削除 (アーカイブ) する方法
既定のテンプレートは、削除することはできませんが、アーカイブしてユーザーに表示されないようにすることはできます。

同様に、カスタム テンプレートを発行した後で、ユーザーが表示できないようにする場合は、テンプレートを編集し、**[構成]** ページから **[アーカイブ]** および **[保存]** を選択します。 または、**[テンプレート]** ページからテンプレートを選択し、**[アーカイブ]** を選択します。

既定のテンプレートは編集できないので、これらのテンプレートをアーカイブするには、**[テンプレート]** ページの **[アーカイブ]** オプションを使用する必要があります。 Outlook の **[転送不可]** オプションをアーカイブすることはできません。

#### 既定のテンプレートを削除するには

-   **[テンプレート]** ページで、既定のテンプレートを選択し、**[アーカイブ]** をクリックします。

ステータスが **[発行済み]** から **[アーカイブ済み]** に変更されます。 変更する場合は、テンプレートを選択し、**[発行]** をクリックします。

## <a name="BKMK_RefreshingTemplates"></a>ユーザー用のテンプレートの更新
Azure RMS を使用する場合、テンプレートは自動的にクライアント コンピューターにダウンロードされるので、ユーザーはアプリケーションからテンプレートを選択できます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。

|アプリケーションまたはサービス|変更後のテンプレートの更新方法|
|-------------------|-------------------|
|Exchange Online|テンプレートを更新するには、手動構成が必要です。<br /><br />構成手順については、「[Exchange Online のみ:変更されたカスタム テンプレートをダウンロードするように Exchange を構成する方法](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_ExchangeOnlineTemplatesUpdate)」セクションを展開してください。|
|Office 365|自動更新: 追加の手順は必要ありません。|
|Office 2016 と Office 2013:<br /><br />Windows 用 RMS 共有アプリケーション|自動更新: スケジュールどおりに更新されます。<br /><br />-   以降のバージョンの Office の場合:既定の更新間隔は 7 日ごとです。<br />-   Windows 用 RMS 共有アプリケーション:バージョン 1.0.1784.0 以降では、既定の更新間隔は 1 日です。 それ以前のバージョンでは、既定の更新間隔は 7 日ごとです。<br /><br />このスケジュールより前に強制的に更新する方法については、後の「[Office 2016、Office 2013、Windows 用 RMS 共有アプリケーション:変更されたカスタム テンプレートを強制的に更新する方法](#BKMK_Office2013ForceUpdate)」セクションを展開してください。|
|Office 2010|ユーザーがログオンしたときに更新されます。<br /><br />強制的に更新するには、ログオフしてもう一度ログオンするようにユーザーに依頼します。 または、以下の「[Office 2010 のみ:変更されたカスタム テンプレートを強制的に更新する方法](#BKMK_Office2010ForceUpdate)」セクションをご覧ください。|
RMS 共有アプリケーションを使用している モバイル デバイスの場合、テンプレートは自動的にダウンロードされるので (必要な場合はさらに更新されます)、追加の構成は必要ありません。

### <a name="BKMK_ExchangeOnlineTemplatesUpdate"></a>Exchange Online のみ:変更されたカスタム テンプレートをダウンロードするように Exchange を構成する方法
Exchange Online 用の Information Rights Management (IRM) を既に構成している場合は、Exchange Online で Windows PowerShell を使用して、次の変更を加えるまでカスタム テンプレートはユーザーにダウンロードされません。

> [!NOTE]
> Exchange Online で Windows PowerShell を使用する方法の詳細については、「[Exchange Online による PowerShell の使用](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx)」を参照してください。

テンプレートを変更するたびにこの手順を実行する必要があります。

##### Exchange Online 用のテンプレートを更新するには

1.  Exchange Online で Windows PowerShell を使用し、サービスに接続します。

    1.  Office 365 のユーザー名とパスワードを入力します。

        ```
        $Cred = Get-Credential
        ```

    2.  Exchange Online サービスに接続するには、次の 2 つのコマンドを実行します。

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) コマンドレットを使用して、信頼された発行ドメイン (TPD) を Azure RMS から再インポートします。

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    たとえば、TPD 名が **RMS Online - 1** である場合 (多くの組織の一般的な名前です)、次のように入力します。**Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > TPD 名を確認するには、[Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) コマンドレットを使用できます。

3.  テンプレートが正常にインポートされたことを確認するには、数分待ってから、[Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) コマンドレットを実行し、[種類] を [すべて] に設定します。 例:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > 出力のコピーを残しておくと、後でテンプレートを保存する場合にテンプレート名または GUID を簡単にコピーできて便利です。

4.  インポートしたテンプレートのうち、Outlook Web App で使用できるようにするテンプレートごとに、[Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) コマンドレットを使用して、[種類] を [分散] に設定する必要があります。

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Outlook Web Access は UI を 24 時間キャッシュするため、ユーザーには最長 1 日間新しいテンプレートが表示されない可能性があります。

さらに、テンプレート (カスタムまたは既定) がアーカイブされ、Exchange Online と Office 365 が使用されている場合、ユーザーが Outlook Web App または Exchange ActiveSync プロトコルを使用するモバイル デバイスを使用する場合、ユーザーはアーカイブされたテンプレートを引き続き表示できます。

これらのテンプレートがユーザーに表示されないようにするには、Exchange Online の Windows PowerShell を使用してサービスに接続し、次のコマンドを実行して [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) コマンドレットを使用します。

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### <a name="BKMK_Office2013ForceUpdate"></a>Office 2016、Office 2013、Windows 用 RMS 共有アプリケーション:変更されたカスタム テンプレートを強制的に更新する方法
Office 2016、Office 2013 または Windows 用 Rights Management (RMS) 共有アプリケーションを実行しているコンピューター上でレジストリを編集すると、変更されたテンプレートがコンピューター上で、既定値よりも短い周期で更新されるように自動スケジュールを変更できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターを誤って使用すると、深刻な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 マイクロソフトは、レジストリ エディターを誤って使用したために発生した問題を解決できることを保証できません。 レジストリ エディターは、各自の責任で使用してください。

##### 自動スケジュールを変更するには

1.  レジストリ エディターを使用して、次のレジストリ値のいずれかを作成し設定します。

    -   更新頻度を日単位で設定するには (最短 1 日):**TemplateUpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の表を使用します。

        |レジストリ パス|型|値|
        |------------|-----|-----|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   更新頻度を秒単位で設定するには (最短 1 秒):**TemplateUpdateFrequencyInSeconds** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (秒数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の表を使用します。

        |レジストリ パス|型|値|
        |------------|-----|-----|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    これらのレジストリ値の両方ではなく、一方のみを作成して設定するようにしてください。 両方が存在する場合、**TemplateUpdateFrequency** は無視されます。

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションとエクスプローラーのインスタンスを再起動します。

##### 直ちに更新するには

1.  レジストリ エディターを使用して、**LastUpdatedTime** 値のデータを削除します。 たとえば、このデータに **2015-04-20T15:52** が表示されている場合、この 2015-04-20T15:52 を削除して、データが表示されないようにします。 このレジストリ値データを削除する際にレジストリ パスを検索するには、次の表を使用します。

    |レジストリ パス|型|値|
    |------------|-----|-----|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\&lt;MicrosoftRMS_FQDN&gt;\Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > レジストリ パスでは、*&lt;MicrosoftRMS_FQDN&gt;* は、Microsoft RMS サービスの FQDN を指します。 この値を確認するには:
    > 
    > 1.  Azure RMS 用の [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) コマンドレットを実行します。 Azure RMS 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。
    > 2.  出力から、**LicensingIntranetDistributionPointUrl** の値を確認します。
    > 
    >     例:**LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  この値から、**https://** 文字列と **/_wmcs/licensing** 文字列を削除します。 残りの値が、Microsoft RMS サービスの FQDN です。 この例では、Microsoft RMS サービスの FQDN は次の値になります。
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  **%localappdata%\Microsoft\MSIPC\Templates** フォルダーとその中に含まれているすべてのファイルを削除します。

3.  Office アプリケーションとエクスプローラーのインスタンスを再起動します。

### <a name="BKMK_Office2010ForceUpdate"></a>Office 2010 のみ:変更されたカスタム テンプレートを強制的に更新する方法
Office 2010 を実行するコンピューター上でレジストリを編集することで、ユーザーがログオフしてもう一度ログオンするまで待たなくても、変更されたテンプレートがコンピューター上で更新されるように値を設定できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターを誤って使用すると、深刻な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 マイクロソフトは、レジストリ エディターを誤って使用したために発生した問題を解決できることを保証できません。 レジストリ エディターは、各自の責任で使用してください。

##### 更新頻度を変更するには

1.  レジストリ エディターを使用して、**UpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の表を使用します。

    |レジストリ パス|型|値|
    |------------|-----|-----|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションを再起動します。

##### 直ちに更新するには

1.  レジストリ エディターを使用して、**LastUpdatedTime** 値のデータを削除します。 たとえば、このデータに **2015-04-20T15:52** が表示されている場合、この 2015-04-20T15:52 を削除して、データが表示されないようにします。 このレジストリ値データを削除する際にレジストリ パスを検索するには、次の表を使用します。

    |レジストリ パス|型|値|
    |------------|-----|-----|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  **%localappdata%\Microsoft\MSIPC\Templates** フォルダーとその中に含まれているすべてのファイルを削除します。

3.  Office アプリケーションを再起動します。

## <a name="BKMK_PowerShellTemplates"></a>Windows PowerShell リファレンス
Azure  クラシック ポータルでテンプレートを作成および管理するためにできることはすべて、Windows PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。

エクスポートとインポートを使用して、カスタム テンプレートをバックアップおよび復元することもできます。ベスト プラクティスとして、意図しない変更を行った場合に以前のバージョンに簡単に戻すことができるように、カスタム テンプレートを定期的にバックアップします。

> [!IMPORTANT]
> Windows PowerShell を使用して Azure RMS 権限ポリシー テンプレートを作成および管理するには、[Azure RMS 用の Windows PowerShell モジュール](http://go.microsoft.com/fwlink/?LinkId=257721)のバージョン 2.0.0.0 以降が必要です。
> 
> 既にこの Windows PowerShell モジュールがインストールされている場合は、PowerShell ウィンドウで `(Get-Module aadrm -ListAvailable).Version` コマンドを実行してバージョン番号をご確認ください。

インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。

テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## 次の手順
Azure Rights Management のカスタム テンプレートを構成したら、[Azure Rights Management の展開ロードマップ](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) を使用して、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] をユーザーと管理者にロールアウトする前に他に実行する構成手順があるかどうか確認します。 他の構成手順を実行する必要がない場合は、「[Azure Rights Management を使用する](../Topic/Using_Azure_Rights_Management.md)」で運用ガイダンスを参照し、組織での展開を正常に完了するのに役立ててください。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


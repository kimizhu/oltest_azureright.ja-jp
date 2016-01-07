---
description: na
keywords: na
pagetitle: RMS for Individuals and Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
---
# 個人用 RMS と Azure Rights Management
個人用 RMS は組織内のユーザーを対象にした無料のセルフサービス サブスクリプションです。Azure Rights Management (Azure RMS) によって保護された機密ファイルが組織内のユーザーに送信されているが、IT 部門が Azure でそれらのユーザーのアカウントを管理していないために、該当するユーザーを認証できないという場合に使用できます。 たとえば、IT 部門が Office 365 を所有しておらず、Azure サービスも使用していない場合が挙げられます。

このようなユーザーは、Azure RMS で使用する無料の企業または学校アカウントにサインアップし、Rights Management 共有アプリケーションをダウンロードしてインストールすることができます。 その結果、これらのユーザーは、認証され、保護されたファイルが送信されたユーザーであることが証明されるため、コンピューターまたはモバイル デバイス上で保護されたファイルを読み取ることができます。

Windows コンピューター上で Rights Management 共有アプリケーションを使用すれば、保存されているファイルを保護したり、保護したファイルを組織の内外の宛先に電子メールで送信したりすることができます。 それらのユーザーが送信した電子メールの受信者が属する組織も Azure でユーザー アカウントを管理していない場合、受信者も個人用 RMS アカウントにサインアップすれば、保護された電子メールの添付ファイルを読み取ることができます。

> [!IMPORTANT]
> この無料のサブスクリプションによって、承認されたユーザーはいつでも保護されているファイルを読み取ることができます。 現在は、この無料サブスクリプションを使用して、ドキュメントを保護し、保護された電子メール メッセージを新しく作成することもできますが、保護されたコンテンツを新規作成する機能は試用目的でのみ提供されており、将来的に削除される可能性があります。 個人用 RMS を使用したコンテンツ保護の詳細および変更点については、「[Microsoft Rights Management サービス条件](https://portal.aadrm.com/Legal/Service)」を参照してください。

無料の Rights Management 共有アプリケーションを使用してファイルを保護する方法の詳細については、「[Rights Management 共有アプリケーション ユーザー ガイド](http://technet.microsoft.com/library/dn339006.aspx)」を参照してください。

個人用 RMS は、Azure Active Directory でサポートされているセルフサービス サインアップの一例です。 セルフサービス サインアップのしくみの詳細については、Microsoft Azure ドキュメントの「[Azure のセルフサービス サインアップについて](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)」をご覧ください。 個人用 RMS に固有の詳細な情報については、次のセクションをご覧ください。

-   [個人用 RMS にサインアップする方法](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_SignUp)

    -   [技術的概要](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TechnicalOverview)

-   [個人用 RMS 向けに作成されたアカウントを管理者が制御する方法](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts)

-   [ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法](#BKMK_Detect)

## <a name="BKMK_SignUp"></a>個人用 RMS にサインアップする方法
この無料アカウントにサインアップするには、[Microsoft Rights Management のページ](https://portal.aadrm.com/) にアクセスして企業または学校のメール アドレスを入力して、リクエストを送信します。 このサインアップ ページを表示するための最も一般的な方法は、受信した添付ファイル付きの電子メール メッセージに記載されているサインアップ方法に説明されています。 Microsoft からの応答メールを受信したら、アカウントの作成に必要な詳細情報を入力してサインアップ プロセスを完了できます。 Microsoft から確認の電子メールを取得すると、この最後の電子メール メッセージによって、各種デバイス用の共有アプリケーションをダウンロードできるページと、ユーザー ガイドへのリンクが提供されます。

#### 個人用 RMS にサインアップするには

1.  Windows または Mac コンピューターを使用して、[Microsoft Rights Management](https://portal.aadrm.com) のページに進みます。

2.  組織で使用している電子メール アドレス (**janetm@contoso.com** または **p.dover@fabrikam.com** など) を入力します。

    > [!IMPORTANT]
    > 個人用の電子メール アカウントはサポートされていないため、Microsoft アカウント (以前の Microsoft Live ID アカウント) や、自宅で使用するインターネット プロバイダーから提供されている他の個人アカウントは入力しないてください。

3.  [**作業開始**] をクリックします。

    Microsoft は、電子メール アドレスを使用して、組織が [Azure RMS を含む有料サブスクリプション](https://technet.microsoft.com/library/dn655136.aspx)を既に所有しているかどうかを確認します。 組織が所有している場合、個人用 RMS は必要ないので、すぐにサインインされ、個人用 RMS へのセルフサービス サインアップは取り消されます。 Azure RMS の有料のサブスクリプションが見つからない場合は、次の手順に進みます。

4.  入力したアドレスに確認の電子メール メッセージが届くまで待ちます。 この電子メールは、Microsoft (DoNotReply@microsoft.com) から送信され、件名は「**Microsoft RMS**」です。

5.  確認の電子メールを受け取ったら、指示に含まれるリンクをクリックしてサインアップ プロセスを完了します。

6.  リンクをクリックすると [**Microsoft Rights Management**] ページが開き、アカウントに関する詳細情報を入力できます。 名と姓を入力し、好みのパスワードを入力、確認し、ドロップダウンからお住まいの国 (該当する国が一覧されていない場合は最も近い国) を選び、**[作成]** をクリックします。

7.  作成したアカウントの使用準備が完了したことを通知する電子メール メッセージが Microsoft から届くのを待ちます。

8.  電子メールが届いたら、リンクをクリックしてサインインし、共有アプリケーションをダウンロードしてインストールする手順を読むことができます。または、[ヘルプ] リンクをクリックして、共有アプリケーションのユーザー ガイドを参照できます。

アカウントの作成が完了しました。ファイルの保護を開始したり、他のユーザーが保護しているファイルを読み取ったりすることができます。 ファイルの保護や保護されたファイルの読み取りを行う際にサインインを求められたら、個人用 RMS のアカウントを作成するときに指定した電子メール アドレスとパスワードを入力してください。

### <a name="BKMK_TechnicalOverview"></a>技術的概要
個人用 RMS では、ユーザーの認証に Microsoft のクラウド ベースの技術を使用するその他のサービスによって使用される、セルフサービスのサインアップ プロセスが使用されます。

組織が Office 365 サブスクリプションまたは Azure サブスクリプションを保有していない場合にユーザーが個人用 RMS にサインアップすると、Azure にユーザーを認証するディレクトリがなく、バックグラウンドでは次が発生します。

1.  組織の最初のユーザーが個人用 RMS のサブスクリプションを要求すると、入力された電子メール アドレスのドメイン名が、Azure テナントに既に関連付けられているかどうかがチェックされます。 既存のテナントが存在しない場合は、組織用の新しいテナントと Azure ディレクトリが自動的に作成されます。このとき、この最初のユーザーのアカウントも作成されます。 Azure の有料サブスクリプションとは異なり、この最初のアカウントはグローバル管理者ではなく、標準ユーザーになります。 新しいアカウントでは、ユーザーが指定した電子メール アドレスとパスワードが使用されます。

    > [!NOTE]
    > ディレクトリの作成には使用できないドメイン名が一部あり、それらは個人用 RMS では使用できません。 ブロックされているドメイン名の一覧は、次の JavaScript Object Notation ファイルで確認できます: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    既存のテナントが見つかった場合は、そのテナントが調べられ、Azure RMS のサブスクリプションを既に持っているかどうかが確認されます。 サブスクリプションが見つからない場合は、無料の個人用 RMS サブスクリプションを追加できます。

2.  組織には、個人用 RMS のサブスクリプションが付与されます。 これで、そのユーザーは、Azure によって認証されるようになり、Azure Rights Management を使用してファイルを保護するとともに、他のユーザーが保護しているファイルを読み取ることができるようになります。 ファイルの保護や保護されたファイルの読み取りを行うには、無料の [Rights Management 共有アプリケーション](https://technet.microsoft.com/library/dn919648.aspx)など、RMS 対応アプリケーションを用意する必要があります。

3.  同じ組織に属する 2 人目のユーザーが個人用 RMS サブスクリプションを要求すると、組織の個人用 RMS サブスクリプションを使用して、既に作成済みの Azure ディレクトリに新しいユーザー アカウントが追加されます。 この 2 人目のユーザーは、最初のユーザーが実行できるすべての操作を実行できます (ファイルの保護と保護されたファイルの読み取り)。さらに、これらの 2 人のユーザーは既定のテンプレートをファイルに即座に適用して、組織の Azure ディレクトリのアカウントにアクセス制限を適用することができるため、セキュリティで保護された共同作業を簡単に行えるようになります。

4.  同じ組織に属する以降のユーザーも同様のパターンに従い、組織の Azure ディレクトリに (新しいユーザーがサインアップすると) ユーザー アカウントが追加されます。 ディレクトリに多数のアカウントが追加されると、より多くのユーザーが同僚やパートナーとセキュリティで保護された共同作業を行うことができ、承認されていないユーザーがファイルにアクセスすべきでない場合に、そのファイルを読み取れないように簡単に設定できます。

このプロセス全体を通じて、組織に対して料金が発生することはなく、IT 部門による作業も不要です。 ただし、IT 部門は次のいずれかを行うことを選択できます。

-   **アカウントおよびサインアップ プロセスを管理する**:IT 管理者は、Azure に自動作成されたディレクトリとアカウントの所有権を取得できます。 パスワード同期やシングル サインオンなどのディレクトリ統合ソリューションを実装して、アカウントを管理できます。 または、ユーザーがアカウントの作成または個人用 RMS へのサインアップを行えないようにすることもできます。

    詳細については、「[個人用 RMS 向けに作成されたアカウントを管理者が制御する方法](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts)」セクションを参照してください。

-   **Rights Management の管理**:IT 管理者は、組織の個人用 RMS サブスクリプションを、Azure Rights Management を含む有料サブスクリプションに変換できます。 この処理を行うと、既存の Azure ディレクトリとアカウントを保持しつつ、個人用 RMS を使用していた既存ユーザーをシームレスに移行することができます。 以前に保護していたすべてのファイルは、引き続き同じポリシーで保護され、ファイルの使用権限を付与されているユーザーは同じ方法でファイルを使用できます。

    この手順を選択すると、組織のワークフロー、サービス、およびデータ ストアに Rights Management を統合できるという利点があります。 さらに、組織の Azure Rights Management 用テナント キーを制御できるため、Rights Management を管理できるようになります。 以下を行うことができます。

    -   Exchange や SharePoint がオンプレミスで実行されている場合でも、Azure Rights Management をサポートするように構成できます。 Exchange と SharePoint はオンライン サービスでネイティブにサポートされており、オンプレミス サーバーのコネクタでもサポートされています。 詳細については、以下を参照してください。

        -   トピック「[Azure Rights Management 用にアプリケーションを構成する](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)」の「[Office 365: クライアントとオンライン サービスの構成](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365)」の「Exchange Online」セクションおよび「SharePoint Online」セクション

        -   [Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)

    -   会社が所有するデータの電子情報開示を実行し、必要に応じて、Rights Management を使用して保護されているファイルの暗号化を解除できます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md)」を参照してください。

    -   組織で使用された Rights Management のアクティビティをすべてログに記録できます。 この機能は非常に有用であり、保護されたファイルの監視や、それらのファイルに正常にアクセスしているユーザーの監視だけでなく、未承認のユーザーが保護されたファイルへのアクセスを試行している不審な行為を特定することもできます。 詳細については、「[Azure Rights Management の利用状況をログに記録して分析する](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md)」を参照してください。

    -   保護されたドキュメントの追跡および取り消しの機能が [Azure RMS サブスクリプション](https://technet.microsoft.com/dn858608)でサポートされている場合、ユーザーはそれらの機能を使用できます。 詳細については、「[RMS 共有アプリケーション ユーザー ガイド](https://technet.microsoft.com/library/dn339006.aspx)」の[ファイルの追跡および取り消し](https://technet.microsoft.com/library/dn986611.aspx)をご覧ください。

    -   BYOK (Bring Your Own Key) ソリューションを実装して、組織の IT ポリシーに従って Azure Rights Management のテナント キーをオンプレミスで生成し、そのキーをハードウェア セキュリティ モジュール (HSM) を使用して Microsoft に安全に転送することができます。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」を参照してください。

## <a name="BKMK_TakeControlofAccounts"></a>個人用 RMS 向けに作成されたアカウントを管理者が制御する方法
組織の個人用 RMS サブスクリプションを有料のサブスクリプションに切り替えない場合でも、組織用に作成された Azure ディレクトリのユーザー アカウントを次の方法で制御できます。

-   Azure Active Directory と Active Directory ドメイン サービス インフラストラクチャに対して、ディレクトリ統合ソリューションを実装します。 アカウントとパスワードを同期することで、ユーザーは Rights Management を使用するために新しいアカウントを作成する必要がなくなり、新しい Azure ユーザー アカウントにオンプレミスのパスワード ポリシーが適用されます。 また、パスワードを同期すると、ユーザーは Rights Management を使用するために別のパスワードを覚えておく必要がなくなります。

-   ユーザーがサインアップして個人用 RMS サブスクリプションで Azure Rights Management を使用するのを防ぐことができます。 通常、この方法には利点がほとんどありません。ユーザーは保護なしでファイルを共有するか (会社に対してリスクが生じる可能性があります)、または IT 部門がデータにアクセスできない別のファイル保護メカニズムを使用するかのいずれかを選択することになるためです。 それでも、ユーザーがサインアップできず個人用 RMS を使用できないようにする場合は、Azure での組織のディレクトリの所有権を取得した後に、次のいずれかの操作を実行してください。

    -   すべてのユーザーが、セルフサービス サブスクリプション (個人用 RMS を含む) にサインアップできないようにします。  現時点で、これをサービス別に設定することはできません。設定はセルフサービス プロセスを使用するすべての Azure サブスクリプションに適用されます。 これを適用するには、Azure Active Directory 用の Windows PowerShell モジュールの [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) コマンドレットを使用して、**AllowAdHocSubscriptions** パラメーターを false に設定します。 例: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   ユーザーが Azure に新しいアカウントを作成できないようにします。つまり、Azure に既にアカウントを持っているユーザーしかセルフサービス サブスクリプション (個人用 RMS を含む) にサインアップできないようにします。  これを適用するには、Azure Active Directory 用の Windows PowerShell モジュールの [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) コマンドレットを使用して、**AllowEmailVerifiedUsers** パラメーターを false に設定します。 例: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Active Directory ドメイン サービス インフラストラクチャと Azure Active Directory を同期します。 この操作により、ユーザーが個人用 RMS などのセルフサービス サブスクリプションにサインアップしても新しいアカウントが作成されなくなり、Azure ディレクトリに作成済みのアカウントを削除または無効にすることができます。

Azure ディレクトリ内のユーザー アカウントを制御する、またはユーザーによる個人用 RMS へのサインアップを防ぐには、Azure サブスクリプションがあり、ディレクトリを所有している必要があります。 Azure サブスクリプションをまだ持っていない場合は、無料のサブスクリプションを取得できます。 セルフサービス プロセス中にディレクトリが自動作成された場合は、ディレクトリの作成時に使用されたドメインの所有権を取得します。 Azure にディレクトリを既に所有しているが、組織で使用する新しいドメインがユーザーによって指定された場合、そのドメインを既存のディレクトリにマージしてください。 詳細については、「[Azure のセルフ サービス サインアップについて](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)」の説明をご覧ください。

## <a name="BKMK_Detect"></a>ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法
ユーザーが個人用 RMS にサインアップしたかどうかを、管理者はどのようにして知ることができるでしょうか。 次に示す方法のいずれかを使用する場合もあれば、組み合わせて使用する場合もあります。

-   機密性の高いファイルをどのように保護しているかを (組織外の人物と共同作業している場合は特に) ユーザーにたずねます。

-   組織用の Azure サブスクリプションを所有している場合は、[Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) コマンドレットを使用して、サブスクリプションの 1 つとして **RIGHTSMANAGEMENT_ADHOC** が返されるかどうかを確認します。 返される場合、それは組織に付与された個人向けサブスクリプションの RMS であり、ユーザーがセルフ サービスのサインアップ プロセスで使用できるアクティブなユニットが多数存在します。

-   System Center Configuration Manager などのシステム管理ソリューションを使用して、インストール済みのソフトウェアと使用中のソフトウェアのインベントリを作成します。 Rights Management 共有アプリケーションの実行には、**ipviewer.exe** プログラムが使用されています。また、[アプリケーションを無料でダウンロードしてインストール](http://go.microsoft.com/fwlink/?LinkId=303970)し、このアプリケーションに関するその他の特性を確認して、ソフトウェア インベントリで利用することができます。

-   Rights Management 共有アプリケーションによって作成されるファイル名拡張子を監視します。 .pfile と .ppdf ファイル名拡張子は最もわかりやすい例ですが、他のファイルでは、Rights Management がネイティブで保護しているときに元のファイル名拡張子が変更される場合があります。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003.aspx)」の「[サポートされるファイルの種類とファイル名拡張子](http://technet.microsoft.com/library/dn339003.aspx)」のセクションを参照してください。

## 参照
[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)


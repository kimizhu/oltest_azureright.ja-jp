---
description: na
keywords: na
pagetitle: Migrating from AD RMS to Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
---
# AD RMS から Azure Rights Management への移行
Active Directory Rights Management サービス (AD RMS) のデプロイを Azure Rights Management (Azure RMS) に移行するには、次の命令セットを使用します。 移行後もユーザーは AD RMS を使用して保護されていたドキュメントや電子メール メッセージにアクセスでき、新しく保護されるコンテンツは Azure RMS を使用します。

この AD RMS の移行が組織にとって適切かどうかわからない場合は、次のようにしてください。

-   Azure RMS の概要、Azure RMS で解決できるビジネス上の問題、管理者およびユーザーから見た Azure RMS、Azure RMS のしくみについては、「[Azure Active Directory Rights Management の概要](../Topic/What_is_Azure_Rights_Management_.md)」を参照してください

-   Azure RMS と AD RMS の比較については、「[Azure Rights Management と AD RMS を構成する](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md)」を参照してください

## AD RMS から Azure RMS への移行の前提条件
Azure RMS への移行を始める前に、次の前提条件が満たされていること、および制限事項を理解していることを確認してください。

|要件|詳細情報|
|------|--------|
|サポートされる RMS のデプロイ|Windows Server 2008 から Windows Server 2012 R2 までの AD RMS のすべてのリリースは、Azure RMS への移行をサポートします。<br /><br />-   Windows Server 2008 (x86 または x64)<br />-   Windows Server 2008 R2 (x64)<br />-   Windows Server 2012 (x64)<br />-   Windows Server 2012 R2 (x64) **Note:** Windows Server 2003 で Windows RMS を実行している場合、このバージョンのオペレーティング システムは 2015 年中にサポートが終了します。 このバージョンの RMS は Azure RMS に移行することができます。ただし、このプロセスはオペレーティング システムがサポートされている期間に限りサポートされます。 この問題を回避するには、信頼された発行ドメイン (TPD) をサポート対象のバージョンの AD RMS にインポートした後、RMS 1.0 互換性オプションを使用せずに TPD を再度インポートしてください。 TPD の詳細については、「[信頼された発行ドメイン](http://technet.microsoft.com/library/dd996639%28v=ws.10%29.aspx)」を参照してください。<br />すべての有効な AD RMS トポロジがサポートされます。<br /><br />-   単一フォレスト、単一 RMS クラスター<br />-   単一フォレスト、複数のライセンス専用 RMS クラスター<br />-   複数フォレスト、複数 RMS クラスター **Note:** 既定では、複数の RMS クラスターが 1 つの Azure RMS テナントに移行します。 異なる RMS テナントが必要な場合は、異なる移行として処理する必要があります。 1 つの RMS クラスターからのキーを、複数の Azure RMS テナントにインポートすることはできません。|
|Azure RMS テナント (非アクティブ) など、Azure RMS を実行するためのすべての要件|「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」を参照してください。<br /><br />AD RMS からの移行を行うには、その前に Azure RMS テナントを用意しておく必要がありますが、移行前に Rights Management サービスをアクティブにしないことをお勧めします。 アクティブ化は、AD RMS からキーとテンプレートをエクスポートし、それらを Azure RMS にインポートした後で、移行プロセスによって行われます。 ただし、Azure RMS が既にアクティブ化されている場合でも、AD RMS から移行することはできます。|
|Azure RMS 用の準備:<br /><br />-   オンプレミス ディレクトリと Azure Active Directory の間でのディレクトリ同期<br />-   Azure Active Directory でのメールが有効なグループ|「[Azure Rights Management の準備を行う](../Topic/Preparing_for_Azure_Rights_Management.md)」を参照してください。|
|AD RMS で Exchange Server (たとえば、トランスポート ルールと Outlook Web Access) または SharePoint Server の Information Rights Management (IRM) 機能を使用していた場合:<br /><br />-   短時間これらのサーバーで IRM が利用できなくなることを予定しておきます。|移行後は Azure RMS を使用してこれらのサーバーで IRM を引き続き使用できます。 ただし、移行手順には、IRM サービスの一時的な無効化、コネクタのインストールと構成、サーバーの再構成、IRM の再有効化が含まれます。<br /><br />移行プロセス中にサービスが中断するのはこのときだけです。|
制限事項:

-   移行プロセスは、サーバー ライセンス証明書 (SLC) キーから Azure RMS のハードウェア セキュリティ モジュール (HSM) への移行をサポートしていますが、Exchange Online では現時点ではこの構成はサポートされていません。Azure RMS への移行後に Exchange Online で完全な IRM 機能を使用する場合は、ご使用の Azure RMS テナント キーが[マイクロソフトによって管理](http://technet.microsoft.com/library/dn440580.aspx)される必要があります。または、Azure RMS テナントがユーザーにより管理される場合 (BYOK)、Exchange Online では IRM の機能を制限付きで実行できます。Exchange Online と Azure RMS の使用に関する詳細については、「[Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration)」を参照してください。

-   Azure RMS でサポートされていないソフトウェアおよびクライアントは、Azure RMS によって保護されているコンテンツを保護したり使用したりすることはできません。 「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」トピックの、サポートされるアプリケーションおよびクライアントのセクションを確認してください。

-   オンプレミスのキーをアーカイブとして Azure RMS にインポートし (インポート プロセス中に TPD をアクティブには設定しないでください)、バッチ内のユーザーを段階的に移行する場合は、AD RMS のユーザーは、移行されたユーザーにより新規に保護されたコンテンツにアクセスすることはできません。 この場合は、可能な限り短い移行時間で論理バッチ内のユーザーを移行します。これにより、関連付けられたユーザーが一緒に移行されます。

    インポート処理中に TPD をアクティブにした場合は、すべてのユーザーが同じキーを使用してコンテンツを保護するため、この制限は適用されません。 すべてのユーザーを個別に自分のペースで移行できるため、この構成を使用することをお勧めします。

-   外部のパートナーと (たとえば、信頼されたユーザー ドメインやフェデレーションを使用して) コラボレーションしている場合は、同時にまたは可能な限り速やかにパートナーも Azure RMS に移行する必要があります。 移行前に AD RMS を使用して保護されていたコンテンツに引き続きアクセスするには、外部パートナーも同じようにこのドキュメントで説明されているクライアント構成の変更を行う必要があります。

    パートナーの構成は異なる可能性があるので、このドキュメントで再構成を正確に説明することはできません。 詳しくは、Microsoft カスタマー サポート サービス (CSS) に問い合わせてください。

## AD RMS から Azure RMS への移行の手順

|移行手順|詳細情報|
|--------|--------|
|**1. Azure RMS 管理ツールをダウンロードする**|手順については、「[Step 1: Download the Azure Rights Management Administration Tool](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step1Migration)」を参照してください。|
|**2. AD RMS から構成データをエクスポートし、それを Azure RMS にインポートする**|構成データ (キー、テンプレート、URL) を AD RMS から XML ファイルにエクスポートした後、Import-AadrmTpd Windows PowerShell コマンドレットを使用してそのファイルを Azure RMS にアップロードします。 AD RMS のキー構成によっては、追加の手順が必要になる可能性があります。<br /><br />-   ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行:AD RMS の一元管理されたパスワード ベースのキーを、マイクロソフト管理の Azure RMS テナント キーに移行します。 これは、最も簡単な移行パスであり、追加の手順は必要ありません。<br />-   HSM で保護されているキーから HSM で保護されているキーへの移行:AD RMS 用の HSM により保存されているキーを、顧客管理の Azure RMS テナント キーに移行します (“Bring Your Own Key” つまり BYOK シナリオ)。 これには、オンプレミス Thales HSM から Azure RMS HSM にキーを転送する追加手順が必要です。<br />-   ソフトウェアで保護されているキーから HSM で保護されているキーへの移行:AD RMS の一元管理されたパスワード ベースのキーを、顧客が管理する Azure RMS テナント キーに移行します (“bring your own key” つまり BYOK シナリオ)。 最初にソフトウェア キーを抽出してオンプレミス HSM にインポートした後、オンプレミス Thales HSM から Azure RMS HSM にキーを転送する追加手順が必要になるため、必要な構成はこの方法が最も多くなります。<br /><br />手順については、「[Step 2. Export configuration data from AD RMS and import it to Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step2Migration)」を参照してください。|
|**3. RMS テナントをアクティブ化する**|可能であれば、インポート処理の前ではなく後に、この手順を実行します。<br /><br />詳細と手順については、「[Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration)」を参照してください。|
|**4. インポートされたテンプレートを構成する**|権限ポリシー テンプレートをインポートするときに、それらの状態がアーカイブされます。 ユーザーが権限ポリシー テンプレートを表示および使用できるようにする場合は、Azure クラシック ポータルでテンプレートの状態を公開に変更する必要があります。<br /><br />手順については、「[Step 4. Configure imported templates](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step4Migration)」を参照してください。|
|**5. Azure RMS を使用するようにクライアントを再構成する**|既存の Windows コンピューターを、AD RMS ではなく Azure RMS サービスを使用するように再構成する必要があります。 この手順は、自分の組織内のコンピューターに適用されるだけでなく、AD RMS を実行していた間に外部パートナーとコラボレーションしていた場合はパートナー組織のコンピューターにも適用されます。<br /><br />また、iOS 搭載の携帯電話や iPad、Android 端末およびタブレット、Windows Phone、Mac コンピューターなどのモバイル デバイスをサポートする[モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイした場合、これらのクライアントが AD RMS を使用するようにリダイレクトした SRV レコードを DNS から削除する必要があります。<br /><br />手順については、「[Step 5. Reconfigure clients to use Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step5Migration)」を参照してください。|
|**6. IRM と Exchange Online の統合を構成する**|Exchange Online で Azure RMS を使用する場合、この手順は必須です。<br /><br />手順については、「[Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration)」を参照してください。|
|**7. RMS コネクタをデプロイする**|次のようなオンプレミス サービスを Azure RMS で使用する場合は、この手順が必要です。<br /><br />-   Exchange Server (たとえば、トランスポート ルールおよび Outlook Web Access)<br />-   SharePoint Server<br />-   ファイル分類インフラストラクチャを実行している Windows Server<br /><br />手順については、「[手順 7. AD RMS の使用を停止する](#BKMK_Step7Migration)」を参照してください。|
|**8. AD RMS の使用を停止する**|すべてのクライアントが Azure RMS を使用していて、AD RMS サーバーにアクセスしていないことを確認した後、AD RMS のデプロイの使用を停止できます。<br /><br />手順については、「[手順 8. Azure RMS テナント キーを更新する](#BKMK_Step8Migration)」を参照してください。|
|**9. Azure RMS テナント キーを更新する**|この手順は、移行前に Cryptographic Mode 2 を実行していなかった場合に必要であり、必須ではありませんが、Azure RMS テナント キーのセキュリティを保護するためすべての移行に対して推奨されます。<br /><br />手順については、「[Step 9. Re-key your Azure RMS tenant key](#BKMK_Step9Migration)」を参照してください。|

### <a name="BKMK_Step1Migration"></a>手順 1:Azure Rights Management Administration Tool をダウンロードする
Microsoft ダウンロード センターに移動し、[Azure Rights Management Administration Tool](http://go.microsoft.com/fwlink/?LinkId=257721) をダウンロードします。このファイルには、Windows PowerShell 用の Azure RMS 管理モジュールが含まれています。

### <a name="BKMK_Step2Migration"></a>手順 2. AD RMS から構成データをエクスポートし、それを Azure RMS にインポートする
この手順は、2 段階の処理です。

1.  信頼された発行ドメイン (TPD) を .xml ファイルにエクスポートすることによって、AD RMS から構成データをエクスポートします。 このプロセスは、すべての移行について同じです。

2.  構成データを Azure RMS にインポートします。 現在の AD RMS のデプロイ構成と、Azure RMS テナント キーに対する優先トポロジに応じて、この手順のプロセスは異なります。

#### 構成データを AD RMS からエクスポートする
すべての AD RMS クラスター上の、組織のコンテンツを保護していたすべての信頼された発行ドメインに対して、次の手順を実行します。 ライセンス専用クラスターでこれを実行する必要はありません。

> [!NOTE]
> Windows Server 2003 Rights Management を使用している場合は、これらの手順ではなく、「[Windows RMS から異なるインフラストラクチャの AD RMS への移行](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)」トピックの「[SLC、TUD、TPD、および RMS の秘密キーのエクスポート](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)」の手順を実行してください。

###### 構成データ (信頼された発行ドメインの情報) をエクスポートするには

1.  AD RMS の管理権限を持つユーザーとして AD RMS クラスターにログオンします。

2.  AD RMS 管理コンソール (**Active Directory Rights Management サービス**) から、AD RMS クラスター名を展開し、**[信頼ポリシー]** を展開し、**[信頼された発行ドメイン]** をクリックします。

3.  結果ウィンドウで信頼された発行ドメインを選択し、操作ウィンドウから [**信頼された発行ドメインのエクスポート**] をクリックします。

4.  **[信頼された発行ドメインのエクスポート]** ダイアログ ボックスで:

    -   **[名前を付けて保存]** をクリックし、パスとファイル名を指定して保存します。 ファイル名の拡張子としては必ず **.xml** を指定します (自動的には付加されません)。

    -   強いパスワードを指定して確認します。 このパスワードを覚えておいてください。後で、構成データを Azure RMS にインポートするときに必要になります。

    -   信頼されたドメイン ファイルを RMS バージョン 1.0 で保存するチェック ボックスをオンにしないでください。

信頼された発行ドメインをすべてエクスポートしたら、このデータを Azure RMS にインポートする手順を開始できます。

#### 構成データを Azure RMS にインポートする
正確な手順は、現在の AD RMS のデプロイ構成と、Azure RMS テナント キーの優先トポロジによって異なります。

現在の AD RMS のデプロイでは、次のいずれかの構成をサーバー ライセンス証明書 (SLC) キーに使用します。

-   AD RMS データベースでのパスワード保護。 これが既定の構成です。

-   Thales ハードウェア セキュリティ モジュール (HSM) を使用する HSM 保護。

-   Thales 以外のサプライヤーのハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護。

-   外部暗号プロバイダーを使用して保護されたパスワード。

> [!NOTE]
> AD RMS でのハードウェア セキュリティ モジュールの使用に関する詳細については、「[AD RMS でのハードウェア セキュリティ モジュールの使用](http://technet.microsoft.com/library/jj651024.aspx)」を参照してください。

Azure RMS テナント キー トポロジのオプションは、テナント キーをマイクロソフトが管理するか (**マイクロソフト管理**) またはユーザーが自分で管理するか (**顧客管理**) の 2 つです。 顧客管理の Azure RMS テナント キーは、“Bring Your Own Key” (BYOK) と呼ばれることもあり、Thales のハードウェア セキュリティ モジュール (HSM) が必要です。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」の「[テナント キー トポロジを選択する:Microsoft による管理 (既定) または自主管理 (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey)」セクションを参照してください。

> [!IMPORTANT]
> 現在、Exchange Online は Azure RMS BYOK と互換性がありません。  移行後に BYOK を使用し、Exchange Online を使用する場合は、この構成により Exchange Online の IRM 機能が制限されることを理解しておきます。 「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」トピックの「[BYOK の料金と制限事項](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing)」セクションの情報は、移行に最適な Azure RMS テナント キー トポロジの選択に役立ちます。

次の表を参考にして、移行に使用する手順を識別してください。 記載されていない組み合わせはサポートされません。

|現在の AD RMS のデプロイ|選択する Azure RMS テナント キー トポロジ|移行手順|
|--------------------|-------------------------------|--------|
|AD RMS データベースでのパスワード保護|マイクロソフト管理|後で説明される「**ソフトウェアで保護されたキーからソフトウェアで保護されたキーへの移行**」の手順を参照してください。<br /><br />これは最も簡単な移行パスであり、Azure RMS に構成データを転送するだけで済みます。|
|Thales nShield ハードウェア セキュリティ モジュール (HSM) を使用する HSM 保護|お客様が管理 (BYOK)|後で説明される「**HSM で保護されたキーから HSM で保護されたキーへの移行**」の手順を参照してください。<br /><br />BYOK ツールセットが必要であり、キーをオンプレミス HSM から Azure RMS HSM に転送した後、構成データを Azure RMS に転送する 2 つの手順で行います。|
|AD RMS データベースでのパスワード保護|お客様が管理 (BYOK)|後で説明される「**ソフトウェアで保護されたキーから HSM で保護されたキーへの移行**」の手順を参照してください。<br /><br />この手順には BYOK ツールセットが必要です。最初にソフトウェア キーを抽出してオンプレミス HSM にインポートし、次にオンプレミス HSM から Azure RMS HSM にキーを転送した後、最後に構成データを Azure RMS に転送する、という 3 つの手順で行います。|
|Thales 以外のサプライヤーのハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護|お客様が管理 (BYOK)|この HSM から Thales nShield ハードウェア セキュリティ モジュール (HSM) にキーを転送する方法については、HSM のサプライヤーに問い合わせてください。 後で説明される「**HSM で保護されたキーから HSM で保護されたキーへの移行**」の手順に従います。|
|外部暗号プロバイダーを使用して保護されたパスワード|お客様が管理 (BYOK)|Thales nShield ハードウェア セキュリティ モジュール (HSM) にキーを転送する方法については、暗号プロバイダーのサプライヤーに問い合わせてください。 後で説明される「**HSM で保護されたキーから HSM で保護されたキーへの移行**」の手順に従います。|
これらの手順を開始する前に、信頼された発行ドメインをエクスポートしたときに作成した .xml ファイルにアクセスできることを確認します。 たとえば、これらは AD RMS サーバーからインターネットに接続されたワークステーションに移動する USB ドライブに保存されている可能性があります。

> [!NOTE]
> ただし、このデータは秘密キーを含むので、これらのファイルを保存し、セキュリティのベスト プラクティスを使用して保護します。

##### ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行
AD RMS 構成を Azure RMS にインポートするにはこの手順を使用します。結果はマイクロソフト管理の Azure RMS テナント キーです。

###### 構成データを Azure RMS にインポートするには

1.  インターネットに接続されたワークステーションで、Windows PowerShell module for Azure RMS (バージョン 2.1.0.0 以降) をダウンロードしてインストールします。[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) コマンドレットが含まれます。

    > [!TIP]
    > 事前にモジュールをダウンロードしてインストールしてある場合は、`(Get-Module aadrm -ListAvailable).Version` を実行してバージョン番号を確認します。

    インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。

2.  [**管理者として実行**] オプションを選択して Windows PowerShell を起動し、[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) コマンドレットを使用して Azure RMS サービスに接続します。

    ```
    Connect-AadrmService
    ```
    プロンプトが表示されたら、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] のテナント管理者資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使用します)。

3.  [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) コマンドレットを使用して、最初にエクスポートした信頼された発行ドメイン (.xml) ファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    例: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

4.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 3 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。 例: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration)」に進む準備が完了しました。

##### HSM で保護されているキーから HSM で保護されているキーへの移行
これは、HSM キーと AD RMS 構成を Azure RMS にインポートする 2 段階の手順で、結果はお客様が管理 (BYOK) する Azure RMS テナント キーです。

最初に Azure RMS に転送できるように HSM キーをパッケージ化し、次に構成データと共にインポートする必要があります。

###### パート 1:Azure RMS に転送できるように HSM キーをパッケージ化します。

1.  「[BYOK (Bring Your Own Key) の実装](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK)」の「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」セクションの手順に従います。「**テナント キーを生成して転送する – インターネット経由**」の手順を使用します。例外を次に示します。

    -   「**テナント キーを生成する**」の手順を実行しないでください。それと同等のものが、既に AD RMS のデプロイメントから取得されています。 Thales のインストールから AD RMS サーバーで使用されるキーを識別し、移行中にこのキーを使用する必要があります。 Thales で暗号化されたキー ファイルの名前は通常、サーバー上のローカルな **key_(keyAppName)_(keyIdentifier)** です。

    -   「**テナント キーの Azure RMS への転送**」の手順を実行しないでください。この手順では Add-AadrmKey コマンドが使用されます。  代わりに、エクスポートされた信頼できる発行ドメインをアップロードするとき、Import-AadrmTpd コマンドを使用し、準備した HSM キーを転送します。

2.  インターネットに接続されているワークステーションでは、Windows PowerShell セッションで、Azure RMS サービスに再接続します。

これで、Azure RMS の HSM キーが準備されたので、HSM キー ファイルと AD RMS 構成データをインポートできます。

###### パート 2:HSM キーと構成データを Azure RMS にインポートする

1.  インターネットに接続されたままのワークステーションと Windows PowerShell セッションで、最初にエクスポートした信頼された発行ドメイン (.xml) ファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    例: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

2.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 1 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。  例: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration)」に進む準備が完了しました。

##### ソフトウェアで保護されているキーから HSM で保護されているキーへの移行
3 段階の手順で AD RMS 構成を Azure RMS にインポートし、結果は顧客管理 (BYOK) の Azure RMS テナント キーです。

最初にサーバー ライセンサー証明書 (SLC) キーを構成データから抽出し、キーをオンプレミス Thales HSM に転送した後、HSM キーをパッケージ化して Azure RMS に転送し、構成データをインポートします。

###### パート 1:構成データから SLC を抽出し、オンプレミス HSM にキーをインポートする

1.  「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」トピックの「[BYOK (Bring Your Own Key) の実装](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK)」セクションの次の手順を使用します。

    -   **テナント キーを生成して転送する – インターネット経由**:**インターネット接続ワークステーションを準備する**

    -   **テナント キーを生成して転送する – インターネット経由**:**未接続ワークステーションを準備する**

    手順に従ってテナント キーを生成しないでください。既に、エクスポートされた構成データ (.xml) ファイルに同等のものがあります。 代わりに、コマンドを実行してファイルからこのキーを抽出し、オンプレミス HSM にインポートします。

2.  切断されているワークステーションで、次のコマンドを実行します。

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    北米の場合: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    追加情報:

    -   ImportRmsCentrallyManagedKey パラメーターは、操作が SLC キーのインポートであることを示します。

    -   パスワードをコマンドで指定しないと、指定するように求められます。

    -   KeyIdentifier パラメーターは、キー ファイルの名前を作成するキーのフレンドリ名です。 子文字の ASCII 文字のみを使用する必要があります。

    -   ExchangeKeyPackage パラメーターは、名前の先頭に BYOK-KEK-pkg- が付く地域固有のキー交換キー (KEK) パッケージを指定します。

    -   NewSecurityWorldPackage パラメーターは、名前の先頭に BYOK-SecurityWorld-pkg- が付く地域固有のセキュリティ ワールド パッケージを指定します。

    このコマンドの結果は次のようになります。

    -   HSM のキー ファイル: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   SLC が除去された RMS 構成データ ファイル: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  RMS 構成データ ファイルが複数ある場合は、残りのファイルに手順 2. を繰り返します。

SLC を HSM ベースのキーとして抽出したので、パッケージ化して Azure RMS に転送できます。

###### パート 2:HSM キーをパッケージ化して Azure RMS に転送する

1.  「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」の「[BYOK (Bring Your Own Key) の実装](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK)」セクションの次の手順を使用します。

    -   **テナント キーを生成して転送する – インターネット経由**:**テナント キーの転送を準備する**

    -   **テナント キーを生成して転送する – インターネット経由**:**テナント キーの Azure RMS への転送**

これで、HSM キーを Azure RMS に転送しました。AD RMS 構成データをインポートする準備が整いました。構成データには新しく転送されたテナント キーへのポインターのみが含まれます。

###### パート 3:構成データを Azure RMS にインポートする

1.  インターネットに接続されたワークステーションと Windows PowerShell セッションのままで、SLC が除去された RMS 構成ファイルをコピーします (切断されたワークステーションから、%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  最初のファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    例: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

3.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 2 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。 例: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration)」に進む準備が完了しました。

### <a name="BKMK_Step3Migration"></a>手順 3.  RMS テナントをアクティブ化する
この手順の詳細は「[Rights Management をアクティブにする](../Topic/Activating_Azure_Rights_Management.md)」を参照してください。

> [!TIP]
> Office 365 サブスクリプションがある場合、Office 365 管理センターまたは Azure クラシック ポータルから Azure RMS をアクティブ化できます。 Azure クラシック ポータルを使用することをお勧めします。この管理ポータルを使用して次の手順を完了するためです。

**Azure RMS テナントが既にアクティブ化されている場合はどうすればよいですか。**組織の Azure RMS サービスが既にアクティブ化されている場合は、ユーザーが既に Azure RMS を使用してコンテンツを保護し、AD RMS の既存のキー (およびテンプレート) ではなく、自動的に生成されたテナント キー (および既定のテンプレート) を使用している可能性があります。 これは、イントラネット上で適切に管理されたコンピューターではほとんど起こりません。AD RMS インフラストラクチャ用に自動的に構成されるためです。 ただし、イントラネットへの接続の頻度が低いワークグループのコンピューターでは発生する可能性があります。 残念ながら、このようなコンピューターの識別は困難です。そのため、AD RMS から構成データをインポートする前に、サービスをアクティブ化しないようにお勧めします。

Azure RMS テナントが既にアクティブ化されていて、前述のようなコンピューターを識別できる場合は、手順 5 の説明に従って、それらのコンピューターで CleanUpRMS_RUN_Elevated.cmd スクリプトを実行してください。 このスクリプトを実行すると、それらのコンピューターで強制的にユーザーの環境が再初期化されるため、更新されたテナント キーとインポートされたテンプレートがダウンロードされます。

### <a name="BKMK_Step4Migration"></a>手順 4.  インポートされたテンプレートを構成する
インポートしたテンプレートは**アーカイブ済み**という既定の状態なので、ユーザーが Azure RMS でこれらのテンプレートを使用できるようにする場合は、この状態を**公開済み**に変更する必要があります。

また、AD RMS のテンプレートが **ANYONE** グループを使用していた場合、テンプレートを Azure RMS にインポートすると、このグループは自動的に削除されます。同等のグループまたはユーザーおよび同じ権限を、インポートされたテンプレートに手動で追加する必要があります。 Azure RMS の同等のグループの名前は **AllStaff-&lt;tenant_GUID&gt;@&lt;tenant_name&gt;.onmicrosoft.com** になります。 たとえば、Contoso の場合、このグループは **AllStaff-9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a@contoso.onmicrosoft.com** のようになります。

お使いの AD RMS テンプレートに ANYONE グループが含まれるかどうかわからない場合は、この手順の「[PowerShell script to identify AD RMS templates that include the ANYONE group](#BKMK_ScriptForANYONE)」セクションを展開してサンプルの PowerShell スクリプトをコピーし、それを使用してこれらのテンプレートを識別します。 AD RMS での Windows PowerShell の使用に関する詳細については、「[Using Windows PowerShell to Administer AD RMS (Windows PowerShell を使用した AD RMS の管理)](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)」を参照してください。

Azure クラシック ポータルの既定の権限ポリシー テンプレートの 1 つをコピーした場合、組織の自動作成されたグループが表示され、その後 [**権限**] ページで [**ユーザー名**] を特定できます。 ただし、手動で作成またはインポートしたテンプレートに Azure クラシック ポータルを使用してこのグループを追加することはできないため、代わりに次の Azure RMS PowerShell オプションのいずれかを使用する必要があります。

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell コマンドレットを使用して、"AllStaff" グループおよび権限を権限定義オブジェクトとして定義し、ANYONE グループに加えて元のテンプレートで既に権限を付与されていた他の各グループまたはユーザーに対してこのコマンドを再度実行します。 その後、[Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx) コマンドレットを使用して、これらの権限定義オブジェクトをテンプレートに追加します。

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) コマンドレットを使用して、テンプレートを .XML ファイルにエクスポートします。このファイルを編集して、"AllStaff" グループおよび権限を既存のグループおよび権限に追加してから、[Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) コマンドレットを使用してこの変更を Azure RMS にインポートします。

> [!NOTE]
> この同等グループ "AllStaff" は、AD RMS の ANYONE グループと全く同じではありません。"AllStaff" グループには、Azure テナントのすべてのユーザーが含まれます。一方、ANYONE グループには、認証されたすべてのユーザーが含まれ、組織外のユーザーが含まれる場合があります。
> 
> こうしうた 2 つのグループの違いにより、"AllStaff" グループだけでなく外部ユーザーも追加しなければならない場合があります。 グループの外部の電子メール アドレスは、現在サポートされていません。

AD RMS からインポートしたテンプレートの外観と動作は、Azure クラシック ポータルで作成するカスタム テンプレートと同じです。 インポートしたテンプレートを公開に変更し、ユーザーがアプリケーションからそれらを表示して選択したり、テンプレートにその他の変更を加えたりできるようにする方法は、「[Azure Rights Management のカスタム テンプレートを構成する](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md)」を参照してください。

> [!TIP]
> 移行プロセス中のユーザーに対するエクスペリエンスを一貫したものにするため、これらの 2 つの変更以外に、インポートしたテンプレートを変更しないでください。また、Azure RMS に付属する既定のテンプレートを 2 つ公開したり、この時点で新しいテンプレートを作成したりしないでください。 代わりに、移行プロセスが完了するまで待ち、AD RMS サーバーを使用停止にします。

#### <a name="BKMK_ScriptForANYONE"></a>ANYONE グループを含む AD RMS テンプレートを識別するためのサンプル Windows PowerShell スクリプト
このセクションに含まれるサンプル スクリプトを使用すると、前のセクションで説明したように、ANYONE グループが定義されている AD RMS テンプレートを識別できます。

*&#42;&#42;免責事項:&#42;&#42;このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスではサポートされません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。*

```
import-module adrmsadmin New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force $ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate foreach($Template in $ListofTemplates) { $templateID=$Template.id $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright $templateName=$Template.DefaultDisplayName if ($rights.usergroupname -eq "anyone") { $templateName = $Template.defaultdisplayname write-host "Template " -NoNewline write-host -NoNewline $templateName -ForegroundColor Red write-host " contains rights for " -NoNewline write-host ANYONE  -ForegroundColor Red } } Remove-PSDrive MyRmsAdmin -force
```

### <a name="BKMK_Step5Migration"></a>手順 5.  Azure RMS を使用するようにクライアントを再構成する
Windows クライアントの場合:

1.  [移行スクリプトをダウンロードします](http://go.microsoft.com/fwlink/?LinkId=524619)。

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    これらのスクリプトは、AD RMS ではなく Azure RMS サービスを使用するように Windows コンピューター上の構成をリセットします。

2.  リダイレクト スクリプト (Redirect_OnPrem.cmd) の指示に従って、新しい Azure RMS テナントをポイントするようにスクリプトを変更します。

3.  Windows コンピューターで、ユーザーのコンテキストで管理者特権を使用してこれらのスクリプトを実行します。

モバイル デバイス クライアントおよび Mac コンピューターの場合:

-   [AD RMS モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイするときに作成した DNS SRV レコードを削除します。

#### 移行スクリプトによって行われる変更
ここでは、移行スクリプトが行う変更について説明します。 この情報は、参照用、トラブルシューティング用、または変更を自分で行いたい場合に使用できます。

CleanUpRMS_RUN_Elevated.cmd:

-   %userprofile%\AppData\Local\Microsoft\DRM および %userprofile%\AppData\Local\Microsoft\MSIPC フォルダーの内容を、すべてのサブフォルダーおよび長い名前のファイルも含めて削除します。

-   次のレジストリ キーの内容を削除します。

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   次のレジストリ値を削除します。

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   次の各場所の下に、パラメーターとして指定された各 URL の次のレジストリ値を作成します。

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    各エントリには、**https://OldRMSserverURL/_wmcs/licensing** の REG_SZ 値が含まれ、**https://&lt;YourTenantURL&gt;/_wmcs/licensing** という形式のデータが含まれます。

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* の形式は、**{GUID} .rms. [地域].aadrm.com** です。
    > 
    > 例:5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Azure RMS の [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) コマンドレットを実行するときに **RightsManagementServiceId** 値を識別することによって、この値を見つけることができます。

### <a name="BKMK_Step6Migration"></a>手順 6.  IRM と Exchange Online の統合を構成する
事前に AD RMS から Exchange Online に TDP をインポートしていた場合、この TDP を削除して、Azure RMS に移行した後にテンプレートおよびポリシーが競合しないようにする必要があります。 これを行うには、Exchange Online から [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) コマンドレットを使用します。

**マイクロソフト管理の** Azure RMS テナント キー トポロジを選択した場合:

-   「[Azure Rights Management 用にアプリケーションを構成する](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)」トピックの「[Exchange Online: IRM 構成](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline)」セクションを参照してください。 このセクションには、Exchange Online サービスに接続して、Azure RMS からテナント キーをインポートし、Exchange Online の IRM 機能を有効化するために実行する、一般的なコマンドが含まれています。 次の手順を完了した後は、Exchange Online で RMS のすべての機能を使用できます。

**顧客管理 (BYOK) の** Azure RMS テナント キー トポロジを選択した場合:

-   「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」トピックの「[BYOK の料金と制限事項](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing)」セクションでの説明のとおり、Exchange Online では RMS の機能を制限付きで使用できます。

### <a name="BKMK_Step7Migration"></a>手順 7.  RMS コネクタをデプロイする
AD RMS で Exchange サーバーまたは SharePoint サーバーの Information Rights Management (IRM) 機能を使用していた場合、最初にこれらのサーバーで IRM を無効にし、AD RMS の構成を削除する必要があります。 次に、Rights Management (RMS) コネクタをデプロイします。これは、オンプレミス サーバーと Azure RMS の間の通信インターフェイス (リレー) として機能します。

最後にこの手順では、電子メール メッセージを保護するために使用されていた複数の TPD を Azure RMS にインポートした場合、Exchange Server コンピューター上のレジストリを手動で編集して、RMS コネクタにすべての TPD URL をリダイレクトする必要があります。

> [!NOTE]
> 開始する前に、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」トピックの「[Azure RMS をサポートするアプリケーション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications)」セクションの「Azure RMS をサポートするオンプレミス サーバー」で、RMS コネクタがサポートしているオンプレミス サーバーのバージョンを確認してください。

##### Exchange サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  各 Exchange サーバーで次のフォルダーを見つけて、そのフォルダーのすべてのエントリを削除します。\ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  いずれかの Exchange サーバーから、最初に Exchange [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) コマンドレットを使用して、内部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  次に、同じコマンドレットを使用して、外部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  次に、同じコマンドレットを使用して、Microsoft Office Outlook Web App および Microsoft Exchange ActiveSync で IRM を無効にします。

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最後に、同じコマンドレットを使用してキャッシュされている証明書をクリアします。

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  各 Exchange サーバーで、たとえば管理者としてコマンド プロンプトを実行して「**iisreset**」と入力し、IIS をリセットします。

##### SharePoint サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  RMS で保護されたライブラリからドキュメントがチェックアウトされていないことを確認します。 ある場合、この手順の最後でそれらにアクセスできなくなります。

2.  SharePoint サーバーの全体管理 Web サイトの **[サイド リンク バー]** セクションで、**[セキュリティ]** をクリックします。

3.  **[セキュリティ]** ページの **[情報ポリシー]** セクションで、**[Information Rights Management の構成]** をクリックします。

4.  **[Information Rights Management]** ページの **[Information Rights Management]** セクションで、**[このサーバーでは IRM を使用しない]** を選択して、**[OK]** をクリックします。

5.  各 SharePoint サーバー コンピューターで、\ProgramData\Microsoft\MSIPC\Server\*&lt;SharePoint サーバーを実行するアカウントの SID&gt;* フォルダーの内容を削除します。

##### RMS コネクタのインストールと構成

-   「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」トピックの説明に従います。

##### Exchange のみで複数の TPD の場合:レジストリを編集します。

-   各 Exchange サーバーで、インポートした各追加 TPD に対して次のレジストリ キーを手動で追加し、TPD の URL を RMS コネクタにリダイレクトします。 これらのレジストリ エントリは移行に固有であり、Microsoft RMS コネクタ用のサーバー構成ツールでは追加されません。

    これらのレジストリの編集を行うときは、次の手順を使用します。

    -   *ConnectorFQDN* は、DNS で定義したコネクタの名前に置き換えます。 たとえば、**rmsconnector.contoso.com** です。

    -   オンプレミス サーバーとの通信に HTTP または HTTPS のどちらを使用するようにコネクタを構成しているかにより、コネクタの URL に HTTP または HTTPS プレフィックスを使用してください。

    **Exchange 2013 の場合:**

    |レジストリ パス|型|値|データ|
    |------------|-----|-----|-------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS イントラネット ライセンス URL&gt;/_wmcs/licensing|Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/licensing<br />-   https://&lt;connectorName&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS エクストラネット ライセンス URL&gt;/_wmcs/licensing|Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/licensing<br />-   https://&lt;connectorFQDN&gt;/_wmcs/licensing|
    **Exchange Server 2010 の場合:**

    |レジストリ パス|型|値|データ|
    |------------|-----|-----|-------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS イントラネット ライセンス URL&gt;/_wmcs/licensing|Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。<br /><br />-   http://&lt;connectorName&gt;/_wmcs/licensing<br />-   https://&lt;connectorName&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS エクストラネット ライセンス URL&gt;/_wmcs/licensing|Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。<br /><br />-   http://&lt;connectorName&gt;/_wmcs/licensing<br />-   https://&lt;connectorName&gt;/_wmcs/licensing|

以上の手順を完了した後、「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」トピックの「**次のステップ**」セクションを必ずお読みください。

### <a name="BKMK_Step8Migration"></a>手順 8. AD RMS の使用を停止する
省略可能:サービス接続ポイント (SCP) を Active Directory から削除し、コンピューターがオンプレミス Rights Management インフラストラクチャを検出しないようにします。 これは、レジストリに (たとえば、移行スクリプトを実行して) 構成したリダイレクトのため省略可能です。 サービス接続ポイントを削除するには、[Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479) の AD SCP Register ツールを使用します。

たとえば、[システム正常性レポートの要求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest テーブル](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)、[保護されたコンテンツへのユーザー アクセスの監査](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)などを調べることによって、AD RMS サーバーのアクティビティを監視します。 RMS クライアントがこれらのサーバーと通信していないこと、およびクライアントが Azure RMS を正常に使用していることを確認できたら、これらのサーバーから AD RMS サーバーの役割を削除できます。 専用のサーバーを使用している場合は、クライアントが Azure RMS を使用しない理由を調査するときにサービスの継続性を確保するように、サーバーの再起動が必要となる報告された問題がないことを確認するあめに、最初にサーバーのシャットダウン期間に警告手順を使用してもかまいません。

AD RMS サーバーの使用を停止した後、Azure クラシック ポータルでテンプレートをレビューして統合しユーザーの選択肢を減らしたり、再構成したり、新しいテンプレートを追加したりできます。 これは、既定のテンプレートを発行する絶好のタイミングでもあります。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md)」を参照してください。

### <a name="BKMK_Step9Migration"></a>手順 9.  Azure RMS テナント キーを更新する
これは、AD RMS デプロイで RMS Cryptographic Mode 1 を使用していた場合、移行が完了したときに必要な手順です。キーの更新により RMS Cryptographic Mode 2 を使用する新しいテナント キーが作成されるためです。 Cryptographic Mode 1 での Azure RMS の使用は、移行プロセス中にのみサポートされます。

この手順は省略可能ですが、移行が完了したとき、RMS Cryptographic Mode 2 で実行していた場合でも推奨されます。AD RMS キーに対する潜在的なセキュリティ侵害から Azure RMS テナント キーをセキュリティで保護するのに役立ちます。 Azure RMS テナント キーを更新すると (「キーのローリング」とも呼ばれます)、新しいキーが作成され、元のキーがアーカイブされます。 ただし、キーの移動には数週間かかりすぐには完了しないので、元のキーの侵害が疑われるまで待たず、移行が完了したらすぐに RMS テナント キーを更新してください。

Azure RMS テナント キーを更新するには:

-   RMS テナント キーがマイクロソフト管理の場合:マイクロソフト カスタマー サポート サービス (CSS) を呼び出し、RMS テナント管理者であることを証明します。

-   RMS テナント キーが顧客管理 (BYOK) である場合:BYOK 手順を繰り返して、インターネット経由または手動で新しいキーを生成および作成します。

RMS テナント キーの管理の詳細については、「[Azure Rights Management テナント キーに対する操作](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md)」を参照してください。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


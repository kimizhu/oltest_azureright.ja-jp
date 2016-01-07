---
description: na
keywords: na
pagetitle: Active Directory Rights Management Services Mobile Device Extension
search: na
ms.date: na
ms.tgt_pltfrm: na
ms.assetid: a69ead9d-7dd3-4b38-9830-4728e9757341
robots: noindex,nofollow
---
# Active Directory Rights Management Services モバイル デバイス拡張機能
Active Directory Rights Management サービス (AD RMS) モバイル デバイス拡張機能は、既存の AD RMS 展開の上で動作します。これにより、モバイル デバイスを持っているユーザーは、デバイスが最新の RMS クライアントをサポートし、RMS 対応アプリケーションを使用している場合、機密データを保護して使用できます。たとえば、これらのデバイスのユーザーは次の操作を行うことができます。

-   RMS 共有アプリケーションを使用して、異なる形式 (.txt、.csv、.xml) の保護されたテキスト ファイルを使用する。

-   RMS 共有アプリケーションを使用して、保護されたイメージ ファイル (.jpg、.gif、.tif など) を使用する。

-   RMS 共有アプリケーションを使用して、一般保護されている (.pfile 形式) ファイルを開く。

-   RMS 共有アプリケーションを使用して、デバイス上のイメージ ファイルを保護する。

-   モバイル デバイス用の RMS 対応 PDF ビューアーを使用して、Windows 用 RMS 共有アプリケーションまたは別の RMS 対応アプリケーションで保護された PDF ファイルを開く。

-   RMS をネイティブでサポートされるファイル タイプをサポートする RMS 対応アプリケーションを提供するソフトウェア ベンダーからの他のアプリケーションを使用する。

-   RMS SDK. を使用して作成された内部開発の RMS 対応アプリケーションを使用する。

> [!NOTE]
> RMS 共有アプリケーションは、Microsoft Web サイトの [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) ページからダウンロードできます。
> 
> RMS をサポートするさまざまなファイルの種類の詳細については、「Rights Management 共有アプリケーションの管理者ガイド」の「[サポートされているファイルの種類とファイル名拡張子](http://technet.microsoft.com/library/dn339003.aspx)」セクションを参照してください。

Exchange ActiveSync IRM をサポートするメール アプリケーションを使用しているデバイスで保護された電子メールを使用または作成するには、モバイル デバイス拡張機能は必要ありません。RMS およびモバイル デバイスのこのネイティブ サポートは、Exchange 2010 Service Pack 1 で導入されました。

Active Directory Rights Management サービス (AD RMS) モバイル デバイス拡張機能を展開するには、次のセクションを使用します。

-   [AD RMS モバイル デバイス拡張機能の前提条件](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_Preqs)

    -   [AD RMS モバイル デバイス拡張機能用の AD FS の構成](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)

    -   [AD RMS モバイル デバイス拡張機能用の AD FS の構成](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)

-   [AD RMS モバイル デバイス拡張機能用の DNS SRV レコードの指定](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_SRV)

-   [AD RMS モバイル デバイス拡張機能の展開](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_Deploy)

## <a name="BKMK_Preqs"></a>AD RMS モバイル デバイス拡張機能の前提条件
AD RMS モバイル デバイス拡張機能をインストールする前に、以下の依存関係があることを確認します。

|要件|説明を見る|
|------|---------|
|Windows Server 2012 R2 または Windows Server 2012 上の既存の AD RMS 展開。 **Note:** AD RMS は、同じサーバー上でのテストに使用されることが多い Windows 内部データベースではなく、異なるサーバー上の完全な Microsoft SQL Server ベースのデータベースを使用する必要があります。|AD RMS に関するドキュメントについては、Windows Server ライブラリの「[Active Directory Rights Management サービス](http://technet.microsoft.com/library/hh831364.aspx)」を参照してください。|
|Windows Server 2012 R2 に展開された AD FS|AD FS に関するドキュメントについては、Windows Server ライブラリの「[Windows Server 2012 R2 AD FS の展開ガイド](http://technet.microsoft.com/library/dn486820.aspx)」を参照してください。<br /><br />AD FS をモバイル デバイス拡張機能用に構成する必要があります。手順については、このトピックの「[AD RMS モバイル デバイス拡張機能用の AD FS の構成](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)」セクションを参照してください。|
|DNS の SRV レコード|会社のドメインに 1 つ以上の SRV レコードを作成します。<br /><br />-   ユーザーが使用する電子メール ドメイン サフィックスごとに 1 レコード<br />-   コンテンツを保護するために RMS クラスターによって使用されるすべての FQDN に対して 1 レコード<br /><br />ユーザーがモバイル デバイスから電子メール アドレスを提供する場合は、ドメイン サフィックスを使用して、ユーザーが AD RMS インフラストラクチャまたは Azure RMS を使用する必要があるかどうかを示します。SRV レコードが見つかると、クライアントはその URL に応答する AD RMS サーバーにリダイレクトされます。<br /><br />ユーザーが保護されたコンテンツをモバイル デバイスで使用するとき、クライアント アプリケーションはコンテンツを保護したクラスターの URL の FQDN と一致するレコードを DNS で検索します。その後、デバイスは DNS レコードで指定された AD RMS クラスターに送られて、コンテンツを開くためのライセンスを取得します。ほとんどの場合、RMS クラスターはコンテンツを保護したものと同じ RMS クラスターです。<br /><br />SRV レコードを指定する方法の詳細については、このトピックの「[AD RMS モバイル デバイス拡張機能用の DNS SRV レコードの指定](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_SRV)」セクションを参照してください。|
|現在サポートされているクライアント:<br /><br />-   Android 用 RMS 共有アプリケーションの最新バージョンを使用する Android デバイス|Android 4.0.3 以上。<br /><br />Android 用 RMS 共有アプリケーションを [Microsoft Connect サイト](https://connect.microsoft.com/site1170/Downloads) からダウンロードし、デバイスにサイドローディングします。|

### <a name="BKMK_ADFS"></a>AD RMS モバイル デバイス拡張機能用の AD FS の構成
最初に AD FS を構成した後、Android 用 RMS 共有アプリケーションを承認する必要があります。

##### 手順 1:AD FS を構成するには

-   Windows PowerShell スクリプトを実行して AD RMS モバイル デバイス拡張機能をサポートするための AD FS を自動的に構成するか、または構成オプションと値を手動で指定することができます。

    -   AD FS を自動的に構成するには、以下をコピーして Windows PowerShell スクリプト ファイルに貼り付けた後、実行します。

        ```
        # This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

        # Check if Microsoft Rights Management Mobile Device Extension is configured on the Server 
        $CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
        if ($CheckifConfigured)
        {
        Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
        Write-Host $CheckifConfigured 
        }
        else
        {
        Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

        # TransformaRules used by Microsoft Rights Management Mobile Device Extension
        # Claims: E-mail, UPN and ProxyAddresses
        $TransformRules = @"
        @RuleTemplate = "LdapClaims"
        @RuleName = "Jwt Token"
        c:[Type ==
        "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
        Issuer == "AD AUTHORITY"]
         => issue(store = "Active Directory", types =
        ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
        "http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
        ";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through"
        c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
         => issue(claim = c);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through"
        c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
         => issue(claim = c);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through Proxy addresses"
        c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
         => issue(claim = c);
        "@

        # AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
        # Allow All users
        $AuthorizationRules = @"
        @RuleTemplate = "AllowAllAuthzRule"
         => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit",
        Value = "true");
        "@

        # Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
        Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

        Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
        }
        ```

    -   AD FS を手動で構成するには、次の設定を使用します。

        |構成|［値］|
        |------|-------|
        |**証明書利用者の信頼**|api.rms.rest.com|
        |**要求ルール**|**属性ストア**:Active Directory<br /><br />**電子メール アドレス**:E-Mail-Address<br /><br />**ユーザー プリンシパル名**:UPN<br /><br />**プロキシ アドレス**:https://schemas.xmlsoap.org/claims/ProxyAddresses|

##### 手順 2:Android 用 RMS 共有アプリケーションを承認する

-   Android デバイスのサポートを追加するには、次の Windows PowerShell コマンドを実行します。

    ```
    Add-AdfsClient -Name "RMSsharingAndroid" -ClientId "com.microsoft.ipviewer" -RedirectUri @("com.microsoft.ipviewer://authorize")
    ```

### <a name="BKMK_SRV"></a>AD RMS モバイル デバイス拡張機能用の DNS SRV レコードの指定
ユーザーが使用する各電子メール ドメインに対して DNS SRV レコードを作成する必要があります。すべてのユーザーが 1 つの親ドメインからの子ドメインを使用し、この連続する名前空間のすべてのユーザーが同じ RMS クラスターを使用する場合は、親ドメインの SRV レコードを 1 つだけ使用すれば済みます。RMS が、適切な DNS レコードを検索します。

SRV レコードの形式は次のとおりです。_rmsdisco._http._tcp. *&lt;emailsuffix&gt;**&lt;portnumber&gt;**&lt;RMSClusterFQDN&gt;*

たとえば、組織に次の電子メール アドレスを使用するユーザーがいて、

-   user@contoso.com

-   user@sales.contoso.com

-   user@fabrikam.com

さらに、**rmsserver.contoso.com** という名前の RMS クラスターとは異なる RMS クラスターを使用する、contoso.com の子ドメインが他に存在しない場合、次の値を持つ 2 つの DNS SRV レコードを作成します。

-   _rmsdisco._http._tcp.contoso.com 443 rmsserver.contoso.com

-   _rmsdisco._http._tcp.fabrikam.com 443 rmsserver.contoso.com

電子メール ドメインに対するこれらの DNS SRV レコードに加えて、ユーザー ドメインに別の DNS SRV レコードを作成する必要があります。このレコードでは、コンテンツを保護する RMS クラスターの URL を指定する必要があります。RMS で保護されているすべてのファイルには、そのファイルを保護したクラスターへの URL が含まれます。モバイル デバイスは、DNS SRV レコードと、レコードで指定されている URL FQDN を使用して、モバイル デバイスをサポートできる対応する RMS クラスターを探します。

たとえば、RMS クラスターが **rmsserver.contoso.com** である場合は、次の値を持つ DNS SRV レコードを作成します。**_rmsdisco._http._tcp.rmsserver.contoso.com 443 rmsserver.contoso.com**

## <a name="BKMK_Deploy"></a>AD RMS モバイル デバイス拡張機能の展開
AD RMS モバイル デバイス拡張機能をインストールする前に、前のセクションで示した前提条件が満たされていて、AD FS サーバーの URL がわかっていることを確認します。次に、以下の操作を行います。

1.  [Microsoft Connect サイト](http://go.microsoft.com/fwlink/?LinkId=397245)から AD RMS モバイル デバイス拡張機能をダウンロードします。

2.  Setup.exe を実行して、Active Directory Rights Management サービス モバイル デバイス拡張機能セットアップ ウィザードを開始します。

3.  メッセージが表示されたら、以前に構成した AD FS サーバーの URL を入力します。

4.  ウィザードを完了します。

RMS クラスター内のすべてのノードで、このウィザードを実行します。


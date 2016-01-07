---
description: na
keywords: na
pagetitle: RMS Client Deployment Notes
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
---
# RMS クライアントのデプロイに関する注意事項
Rights Management サービス クライアント (RMS クライアント) バージョン 2 は、MSIPC クライアントとも呼ばれます。 Microsoft Rights Management サービスと通信する Windows コンピューター (オンプレミスまたはクラウド) 用のソフトウェアで、組織内または管理対象外組織内における、アプリケーションとデバイスを行き来する情報へのアクセスや使用を保護することができます。 RMS クライアントは [Windows 用 Rights Management 共有アプリケーション](https://technet.microsoft.com/library/dn919648.aspx)に付属していますが、[必要に応じてダウンロード](http://www.microsoft.com/download/details.aspx?id=38396)することもできます。これはライセンス契約書に同意すれば、サードパーティ製ソフトウェアと一緒に自由に配布できます。これにより、クライアントは Rights Management サービスにより保護されたコンテンツを保護して使用することができます。

このトピックのセクションは次のとおりです。

-   [RMS クライアントの再配布](#BKMK_RedistributeInstaller)

-   [RMS クライアントのインストール](#BKMK_InstallClient)

-   [RMS クライアントに関する質問と回答](#BKMK_QA)

-   [RMS クライアントの設定](#BKMK_Settings)

-   [AD RMS のみ: RMS クライアントによる信頼された AD RMS サーバーの使用を制限する](#BKMK_UsingTrustedServers)

-   [RMS サービスの検出](#BKMK_ServiceDiscovery)

## <a name="BKMK_RedistributeInstaller"></a>RMS クライアントの再配布
RMS クライアントは自由に再配布でき、他のアプリケーションや IT ソリューションにバンドルできます。 アプリケーション開発者やソリューション プロバイダーには、RMS クライアントを再配布する 2 つのオプションがあります。

-   推奨: お使いのアプリケーションに RMS クライアントのインストーラーを組み込み、それをサイレント モード (**/quiet** スイッチ。次のセクションで詳細を説明します) で実行することをお勧めします。

-   RMS クライアントがお使いのアプリケーションの前提条件を満たすことを確認します。 このオプションを使用する場合、ユーザーがアプリケーションを使用する前に、ユーザーのコンピューターにおいてクライアントを追加、インストール、更新する手順をユーザーに提供する必要がある場合があります。

## <a name="BKMK_InstallClient"></a>RMS クライアントのインストール
RMS クライアントは、**setup_msipc_***&lt; arch &gt;***.exe** という名前のインストーラー実行可能ファイルの中に含まれています。ここで、*&lt; arch &gt;* は **x86** (32 ビット クライアント コンピューターの場合) または **x64** (64 ビット クライアント コンピューターの場合) になります。 64 ビット (x64) のインストーラー パッケージでは、64 ビット オペレーティング システムのインストールで実行される 32 ビット アプリケーションとの互換用 32 ビット実行可能ファイルと、ネイティブの 64 ビット アプリケーションをサポートするための 64 ビット ランタイム実行可能ファイルの両方がインストールされます。 32 ビット (x86) インストーラーは、64 ビットの Windows インストールでは実行されません。

> [!NOTE]
> RMS クライアントのインストールには、ローカル コンピューターの Administrators グループのメンバーなど、管理者特権が必要です。

RMS クライアントをインストールするには、次のインストール方法のいずれかを使用します。

-   **サイレント モード。** コマンドライン オプションの一部に **/quiet** スイッチを使用することで、サイレント モードで RMS クライアントをコンピューターにインストールできます。 次の例は、64 ビット クライアント コンピューターでの RMS クライアントのサイレント モード インストールを示しています。

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **対話型モード。** または、RMS クライアントのインストール ウィザードによって提供される GUI ベースのセットアップ プログラムを使用して、RMS クライアントをインストールすることができます。 これを行うには、ローカル コンピューターにコピーまたはダウンロードされたフォルダー内の RMS クライアントのインストーラー パッケージ (**setup_msipc_***&lt; arch &gt;***.exe**) をダブルクリックします。

## <a name="BKMK_QA"></a>RMS クライアントに関する質問と回答
次のセクションには、RMS クライアントについてよく寄せられる質問、およびそれらに対する回答が示されています。

### RMS クライアントはどのオペレーティング システムでサポートされますか。
RMS クライアントは、次のオペレーティング システムでサポートされます。

|Windows Server オペレーティング システム|Windows クライアント オペレーティング システム|
|--------------------------------|--------------------------------|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 SP1 以降|
|Windows Server 2008 (AD RMS のみ)|Windows Vista SP2 以降 (AD RMS のみ)|

### RMS クライアントはどのプロセッサまたはプラットフォームでサポートされますか。
RMS クライアントは、x86 および x64 のコンピューティング プラットフォームでサポートされます。

### RMS クライアントはどこにインストールされますか。
既定では、RMS クライアントは %ProgramFiles%\Active Directory Rights Management Services Client 2.&lt;マイナー バージョン番号&gt; にインストールされます。

### どのファイルが RMS クライアント ソフトウェアに関連したファイルですか。
次のファイルが RMS クライアント ソフトウェアの一部としてインストールされます。

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

これらのファイルに加えて、RMS クライアント インストールにより、44 言語の多言語ユーザー インターフェイス (MUI) のサポート ファイルもインストールされます。 サポートされている言語を確認するには、RMS クライアントのインストールを実行し、インストールが完了したら、既定のパスにある多言語サポート フォルダーの内容を確認します。

### サポートされているオペレーティング システムをインストールする際に、RMS クライアントは既定で含まれますか。
いいえ。 このバージョンの RMS クライアントは、Microsoft Windows オペレーティング システムのサポートされたバージョンを実行しているコンピューターに個別にインストールできる、オプションのダウンロードとして出荷されます。

### RMS クライアントは Microsoft Update によって自動的に更新されますか。
サイレント インストール オプションを使用してこの RMS クライアントをインストールした場合、RMS クライアントは、現在の Microsoft Update の設定を継承します。 GUI ベースのセットアップ プログラムを使用して RMS クライアントをインストールした場合は、RMS クライアントのインストール ウィザードに、Microsoft Update を有効にするかどうかを確認するメッセージが表示されます。

## <a name="BKMK_Settings"></a>RMS クライアントの設定
次のセクションには、RMS クライアントに関する設定情報が含まれています。 この情報は、RMS クライアントを使用するアプリケーションまたはサービスに問題がある場合に役に立つ場合があります。

> [!NOTE]
> 一部の設定は、RMS 対応アプリケーションが、クライアント モードのアプリケーション (Microsoft Word、Outlook、RMS 共有アプリケーションなど)、またはサーバー モードのアプリケーション (SharePoint および Exchange など) として実行するかどうかによって変わります。  次の表では、これらの設定は**クライアント モード**と**サーバー モード**として区別されています。

### RMS クライアントのライセンスはクライアント コンピューターのどこに保存されますか。
RMS クライアントのライセンスはローカル ディスクに格納されます。また、Windows レジストリにも一部の情報がキャッシュされます。

|説明|クライアント モードのパス|サーバー モードのパス|
|------|-----------------|---------------|
|ライセンスの保存場所|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\*&lt;SID&gt;*\|
|テンプレートの保存場所|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\Templates\*&lt;SID&gt;*\|
|レジストリの場所|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*&lt;SID&gt;*|
> [!NOTE]
> *&lt;SID&gt;* は、サーバー アプリケーションを実行しているアカウントのセキュリティ識別子 (SID) です。 たとえば、アプリケーションが組み込みの Network Service アカウントで実行されている場合、*&lt;SID&gt;* をそのアカウントの既知の SID (S-1-5-20) の値に置き換えます。

### RMS クライアントの Windows レジストリ設定
Windows レジストリ キーを使用して、一部の RMS クライアントの構成を設定または変更することができます。 たとえば、AD RMS サーバーと通信する RMS 対応のアプリケーションの管理者は、エンタープライズ サービスの場所を更新する (発行用に現在選択されている AD RMS サーバーを上書きする) ことをお勧めします。これは、Active Directory トポロジ内のクライアント コンピューターの場所により異なります。 または、クライアント コンピューターでの RMS のトレースを有効にすることをお勧めします。これは、RMS 対応アプリケーションで発生する問題のトラブルシューティングに役立ちます。 次の表を使用して、RMS クライアント用に変更できるレジストリ設定を特定します。

|作業|Settings|
|------|------------|
|AD RMS のみ: クライアント コンピューターのエンタープライズ サービスの場所を更新するには|次のレジストリ キーを編集します。<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />    REG_SZ: 既定<br />    **値:**&lt;http または https&gt;:// *RMS_Cluster_Name*/_wmcs/Certification<br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />    REG_SZ: 既定<br />    **値:** &lt;http または https&gt;:// *RMS_Cluster_Name*/_wmcs/Licensing|
|トレースの有効化と無効化|次のレジストリ キーを更新します。<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />    REG_DWORD:Trace<br />    **Value:**トレースを有効にする場合は 1、トレースを無効にする場合は 0 (既定値)|
|テンプレートを更新する頻度 (日単位) を変更するには|TemplateUpdateFrequencyInSeconds 値が設定されていない場合、次のレジストリ値でユーザーのコンピューターでのテンプレートの更新頻度を指定します。  これらの値のどちらも設定されていない場合は、RMS クライアント (バージョン 1.0.1784.0) を使用するアプリケーションがテンプレートをダウンロードする既定の更新間隔は 1 日です。 これより前のバージョンでは、既定は 7 日ごとです。<br /><br />**クライアント モード:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD:TemplateUpdateFrequency<br />    **Value:**ダウンロード間の日数 (最小値は 1) を指定する整数値。<br /><br />**サーバー モード:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt;SID&gt;*<br />    REG_DWORD:TemplateUpdateFrequency<br />    **Value:**ダウンロード間の日数 (最小値は 1) を指定する整数値。|
|テンプレートを更新する頻度 (秒単位) を変更するには **Important:** この設定を指定した場合は、日単位のテンプレート更新値は無視されます。 1 つまたはもう一方 (両方ではありません) を指定します。|次のレジストリ値で、ユーザーのコンピューターでのテンプレートの更新頻度を指定します。 この値または頻度 (日単位) を変更する値 (TemplateUpdateFrequency) が設定されていない場合、RMS クライアント (バージョン 1.0.1784.0) を使用してテンプレートをダウンロードするアプリケーションの既定の更新間隔は 1 日です。 これより前のバージョンでは、既定は 7 日ごとです。<br /><br />**クライアント モード:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD:TemplateUpdateFrequencyInSeconds<br />    **Value:**ダウンロード間の秒数 (最小値は 1) を指定する整数値。<br /><br />**サーバー モード:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt;SID&gt;*<br />    REG_DWORD:TemplateUpdateFrequencyInSeconds<br />    **Value:**ダウンロード間の秒数 (最小値は 1) を指定する整数値。|
|AD RMS のみ: 次の発行要求時に即座にテンプレートをダウンロードするには|テストと評価を行う際は、可能な限り早期に RMS クライアントでテンプレートをダウンロードすることをお勧めします。 これを行うには、次のレジストリ キーを削除します。これにより、RMS クライアントは TemplateUpdateFrequency レジストリ設定によって指定された時間まで待機するのではなく、次の発行要求時に即座にテンプレートをダウンロードします。<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\&lt;サーバー名&gt;\Template **Note:** &lt;サーバー名&gt; は、外部 (corprights.contoso.com) と内部 (corprights) の URL どちらでもかまいません。そのため、2 つの異なるエントリが存在します。|
|AD RMS のみ: フェデレーション認証のサポートを有効にするには|RMS クライアント コンピューターがフェデレーションによる信頼関係を使用して AD RMS クラスターに接続する場合は、フェデレーション ホーム領域を構成する必要があります。<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_SZ:FederationHomeRealm<br />    **Value:**このレジストリ エントリの値は、フェデレーション サービス (たとえば、"https://fs-01.contoso.com") の URI (Uniform Resource Identifier) です。|
|AD RMS のみ: ユーザー入力にフォームベース認証を必要とするパートナーのフェデレーション サーバーをサポートするには|既定では、RMS クライアントはサイレント モードで動作するため、ユーザー入力は必要ありません。 ただし、パートナーのフェデレーション サーバーの場合は、フォームベース認証の使用など、ユーザー入力が必要であるように構成されている場合があります。 このような場合、RMS クライアントがサイレント モードを無視し、フェデレーション認証フォームがブラウザー ウィンドウに表示され、ユーザーに認証を促すメッセージが表示されるようにする必要があります。<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_DWORD:EnableBrowser **Note:** フォームベース認証を使用するようにフェデレーション サーバーが構成されている場合は、このキーは必須です。 Windows 統合認証を使用するようにフェデレーション サーバーが構成されている場合は、このキーは必要ありません。|
|AD RMS のみ: ILS サービスの使用をブロックするには|既定では、RMS クライアントは ILS サービスによって保護されているコンテンツを使用できますが、次のレジストリ キーを設定して、クライアントがこのサービスをブロックするように構成することができます。 このレジストリ キーが設定され、ILS サービスがブロックされている場合、ILS サービスによって保護されたコンテンツを開いて使用しようとすると、次のエラーが表示されます: <br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)。<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD:**DisablePassportCertification**<br />    **Value:**ILS の使用をブロックする場合は 1、ILS の使用を許可する場合は 0 (既定値)|

### RMS クライアントのテンプレートの配布の管理
テンプレートを使用すると、ユーザーと管理者がすばやく Rights Management の保護を適用し、RMS クライアントが RMS サーバーまたはサービスから自動的にテンプレートをダウンロードするように簡単に設定できます。テンプレートを次のフォルダーの場所に配置すると、RMS クライアントは既定の場所からテンプレートをダウンロードするのではなく、このフォルダーに配置したテンプレートをダウンロードします。 その場合でも、RMS クライアントは引き続き、その他の使用可能な RMS サーバーからテンプレートをダウンロードすることができます。

**クライアント モード:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**サーバー モード:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\*&lt;SID&gt;*

このフォルダーを使用する際に、特別な名前付け規則に従う必要はありません。ただし、テンプレートは RMS サーバーまたはサービスによって発行される必要があり、テンプレートのファイル拡張子を .xml にする必要があります。 たとえば、Contoso-Confidential.xml または Contoso-ReadOnly.xml は有効な名前です。

## <a name="BKMK_UsingTrustedServers"></a>AD RMS のみ: RMS クライアントによる信頼された AD RMS サーバーの使用を制限する
ローカル コンピューターの Windows レジストリを次のように変更することで、RMS クライアントが特定の信頼された AD RMS サーバーのみを使用するように制限することができます。

**RMS クライアントが信頼された AD RMS サーバーのみを使用するように制限を有効化するには**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD:AllowTrustedServersOnly

    **Value:**0 以外の値を指定すると、RMS クライアントは TrustedServers リスト、および Azure Rights Management サービスで構成されている指定されたサーバーのみを信頼します。

**信頼された AD RMS サーバーのリストにメンバーを追加するには**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *&lt;URL または HostName&gt;*

    **Value:**このレジストリ キーの場所に追加する文字列値には、DNS ドメイン名の形式 (たとえば、 **adrms.contoso.com**)、または信頼された AD RMS サーバーへの完全な URL (たとえば、 **https://adrms.contoso.com**) のいずれかを指定できます。 指定された URL が **https://** で始まる場合、RMS クライアントは SSL または TLS を使用して、指定した AD RMS サーバーに接続します。

## <a name="BKMK_ServiceDiscovery"></a>RMS サービスの検出
RMS サービスの検出を使用すると、RMS クライアントがコンテンツを保護する前に、通信する RMS サーバーまたはサービスを確認することができます。 サービスの検出は、RMS クライアントが保護されたコンテンツを使用する際にも実行されますが、これはほとんど実行されません。コンテンツにアタッチされたポリシーには優先 RMS サーバーまたはサービスが記載されており、これが失敗した場合に限り、クライアントがサービスの検出を実行するからです。

サービスの検出はまず、オンプレミス バージョンの Rights Management (AD RMS) を検索します。 これが失敗した場合、サービスの検出はクラウド バージョンの Rights Management (Azure RMS) を自動的に検索します。

オンプレミスのデプロイに対してサービスの検出を実行するため、RMS クライアントは次の内容を確認します。

1.  ローカル コンピューターの Windows レジストリ:サービスの検出の設定がレジストリで構成されている場合、これらの設定が最初に試行されます。  既定では、これらの設定はレジストリでは構成されていません。

2.  Active Directory ドメイン サービス: ドメインに参加しているコンピューターは、サービス接続ポイント (SCP) を Active Directory に照会します。 SCP が登録されると、使用する RMS クライアントに対して、RMS サーバーの URL が返されます。

### AD RMS のみ: Active Directory を使用してサーバー側のサービスの検出を有効にする
十分な権限を持つアカウントの場合 (Enterprise Admins および AD RMS サーバーのローカルの管理者)、AD RMS ルート クラスター サーバーをインストール際にサービス接続ポイント (SCP) を自動的に登録することができます。 フォレスト内に SCP が既に存在する場合、新規 SCP を登録する前に、まず既存の SCP を削除する必要があります。

次の手順を使用して、AD RMS をインストールした後に SCP の登録や削除を行うことができます。 手順を開始する前に、アカウントに必要な権限がある (Enterprise Admins および AD RMS サーバーのローカルの管理者) ことを確認します。

##### Active Directory に SCP を登録することによって、AD RMS のサービスの検出を有効にするには

1.  AD RMS サーバーの Active Directory Management サービス コンソールを開きます。

    -   Windows Server 2008 R2 または Windows Server 2008 を使用している場合は、[**開始**]、[**管理ツール**]、[**Active Directory Rights Management サービス**] の順にクリックします。

    -   Windows Server 2012 R2 または Windows Server 2012 を使用している場合は、[**ツール**]、[**Active Directory Rights Management サービス**] の順にクリックします。

2.  AD RMS コンソールで AD RMS クラスターを右クリックし、[**プロパティ**] をクリックします。

3.  [**SCP**] タブをクリックします。

4.  [**SCPを変更する**] チェック ボックスをオンにします。

5.  [**SCP を現在の証明クラスターに設定する**] オプションを選択して、[**OK**] をクリックします。

### Windows レジストリを使用してクライアント側のサービスの検出を有効にする
SCP を使用しない、または SCP が存在しない場合は、RMS クライアントがその AD RMS サーバーを検出できるように、クライアント コンピューターのレジストリを構成できます。

##### Windows レジストリを使用してクライアント側の AD RMS のサービスの検出を有効にするには

1.  Windows のレジストリ エディター (Regedit.exe) を開きます。

    -   クライアント コンピューターの [実行] ウィンドウで **regedit** と入力し、Enter キーを押してレジストリ エディターを開きます。

2.  レジストリ エディターで、 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC** に移動します。

    > [!IMPORTANT]
    > 64 ビット コンピューターで 32 ビット アプリケーションを実行している場合は、パスは次のようになります。
    > **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  ServiceLocation サブキーを作成するには、[**MSIPC**] を右クリックして [**新規**] を選択し、[**キー**] をクリックして [**ServiceLocation**] と入力します。

4.  EnterpriseCertification サブキーを作成するには、[**ServiceLocation**] を右クリックして [**新規**] を選択し、[**キー**] をクリックして [**EnterpriseCertification**] と入力します。

5.  エンタープライズ証明書の URL を設定するには、[**EnterpriseCertification**] サブキーの **(既定)** 値をダブルクリックして、[**文字列の編集** ] ダイアログ ボックスが表示されたら、**[値] データ**に &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Certification と入力し、[**OK**] をクリックします。

6.  EnterprisePublishing サブキーを作成するには、 [**ServiceLocation**] を右クリックして [**新規**] を選択し、[**キー**] をクリックして EnterprisePublishing と入力します。

7.  エンタープライズ発行 URL を設定するには、[**EnterprisePublishing**] サブキーの **(既定)** をダブルクリックして、[**文字列の編集**] ダイアログ ボックスが表示されたら、**[値] データ**に &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Licensing と入力し、[**OK**] をクリックします。

8.  レジストリ エディターを閉じます。

RMS クライアントが Active Directory への照会で SCP を検索できず、SCP がレジストリでも指定されていない場合は、AD RMS のサービスの検出の呼び出しは失敗します。

### ライセンス サーバーのトラフィックのリダイレクト
たとえば、2 つの組織をマージして、一方の組織の古いライセンス サーバーを廃止し、クライアントを新しいライセンス サーバーにリダイレクトする場合など、サービスの検出時にトラフィックをリダイレクトする必要がある場合があります。 または、AD RMS から Azure RMS に移行する場合などです。 ライセンスのリダイレクトを有効にするには、次の手順を使用します。

##### Windows レジストリを使用して RMS ライセンスのリダイレクトを有効にするには

1.  Windows のレジストリ エディター (Regedit.exe) を開きます。

    -   クライアント コンピューターの [実行] ウィンドウで **regedit** と入力し、Enter キーを押してレジストリ エディターを開きます。

2.  レジストリ エディターで、次のいずれかに移動します。

    -   x64 プラットフォームの 64 ビット バージョンの Office の場合: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   x64 プラットフォームの 32 ビット バージョンの Office の場合: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  LicensingRedirection サブキーを作成するには、[**Servicelocation**] を右クリックして [**新規**] を選択し、[**キー**] をクリックして、[**LicensingRedirection**] と入力します。

4.  ライセンスのリダイレクトを設定するには、[**LicensingRedirection**] サブキーを右クリックして[**新規**] を選択し、[**文字列値**] を選択します。  [**名前**] には以前のサーバーのライセンス URL を指定し、[**値**] には新しいサーバーのライセンス URL を指定します。

    たとえば、Contoso.com にあるサーバーからFabrikam.com のサーバーにライセンスをリダイレクトするには、次の値を入力します。

    **名前:** `https://contoso.com/_wmcs/licensing`

    **値:** `https://fabrikam.com/_wmcs/licensing`

    > [!NOTE]
    > 以前のライセンス サーバーでイントラネットとエクストラネットの URL の両方が指定されている場合、新しい名前と値のマッピングは、LicensingRedirection キーの下にこれらの URL の両方に対して設定する必要があります。

5.  リダイレクトする必要のあるすべてのサーバーに対して、前の手順を繰り返します。

6.  レジストリ エディターを閉じます。


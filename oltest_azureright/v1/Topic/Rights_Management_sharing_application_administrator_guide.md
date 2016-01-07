---
description: na
keywords: na
pagetitle: Rights Management sharing application administrator guide
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
---
# Rights Management 共有アプリケーション管理者ガイド
企業ネットワークで Microsoft Rights Management 共有アプリケーションを担当している場合や、『[Rights Management 共有アプリケーション ユーザー ガイド](../Topic/Rights_Management_sharing_application_user_guide.md)』または「[Windows 用 Microsoft Rights Management 共有アプリケーションの FAQ](http://go.microsoft.com/fwlink/?LinkId=303971)」よりも詳細な技術情報が必要な場合は、以下の情報を使用してください。

-   [Microsoft Rights Management 共有アプリケーションの自動デプロイメント](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ScriptedInstall)

    -   [インストールの成功の確認](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)

    -   [アンインストール コマンド](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_uninstallscripted)

    -   [自動更新の抑制](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SuppressAutomaticUpdates)

    -   [Azure RMS のみ:ドキュメント追跡の構成](#BKMK_DocumentTracking)

    -   [AD RMS のみ: 組織内での複数の電子メール ドメインのサポート](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains)

-   [Microsoft Rights Management 共有アプリケーションの技術的概要](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_AdminOverview)

    -   [保護のレベル - ネイティブとジェネリック](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection)

    -   [サポートされているファイルの種類とファイル名拡張子](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes)

    -   [ファイルの既定の保護レベルの変更](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection)

> [!TIP]
> RMS 共有アプリを初めて使用する場合や、詳細情報が必要な場合は、「[RMS で、RMS 共有アプリケーションを使用してすべてのファイルの種類を保護する方法](https://curah.microsoft.com/191031/how-rms-protects-all-file-types-by-using-the-rms-sharing-app)」を参照してください。

RMS 共有アプリケーションは Azure RMS での作業に最適です。このデプロイメント構成では、別の組織のユーザーへの保護された添付ファイルの送信、および電子メール通知やドキュメントの追跡と取り消しなどのオプションがサポートされているためです。  ただし、いくつかの制限はあるものの、オンプレミス バージョンの AD RMS でも使用できます。 Azure RMS と AD RMS でサポートされている機能の包括的な比較については、「[Azure Rights Management と AD RMS の比較](https://technet.microsoft.com/library/jj739831.aspx)」を参照してください。 AD RMS を所有していて、Azure RMS に移行する場合は、「[AD RMS から Azure Rights Management に移行する](https://technet.microsoft.com/library/dn858447.aspx)」を参照してください。

## <a name="BKMK_ScriptedInstall"></a>Microsoft Rights Management 共有アプリケーションの自動デプロイメント
Windows 版の RMS 共有アプリケーションはスクリプト化されたインストールをサポートするため、企業のデプロイメントに適しています。

インストールの前提条件は、コンピューターで Windows 7 Service Pack 1 以降のバージョンを実行していることと、Microsoft Framework Version 4.0 以降がインストールされていることだけです。 Microsoft .NET Framework 4.0 をインストールする必要がある場合は、[Microsoft ダウンロード センターからダウンロードしてインストール](http://www.microsoft.com/download/details.aspx?id=17718)できます。

#### RMS 共有アプリケーションを自動デプロイメント用にダウンロードするには

1.  Microsoft ダウンロード センターの「[Windows 用 Microsoft Rights Management 共有アプリケーション](http://www.microsoft.com/download/details.aspx?id=40857)」ページに移動して、[**ダウンロード**] をクリックします。

2.  必要なファイルを選択してダウンロードします。 クライアント インストール パッケージは 2 つあります。1 つは Windows 64 ビット (Microsoft Rights Management 共有アプリケーション x64.zip)、もう 1 つは Windows 32 ビット (Microsoft Rights Management 共有アプリケーション x86.zip) です。

3.  圧縮されたインストール パッケージから、ダブルクリックするなどして、ファイルを抽出します。 次に、抽出したファイルを、クライアント コンピューターがアクセスできるネットワークの場所にコピーします。

RMS 共有アプリケーションのセットアップ パッケージは、さまざまなデプロイメント シナリオをサポートしており、次のものが含まれます。

|説明|展開シナリオ|
|------|----------|
|Microsoft Online サインイン アシスタント|次のものに必要です。<br /><br />-   Office 2010 および Azure RMS<br />-   Office 2013 および Azure RMS ([2015 年 6 月 9 日付 Office 2013 用更新プログラム](https://support.microsoft.com/kb/3054853) (KB3054853) をインストールしていない場合)|
|Office 用の修正プログラム (KB 2596501)|次のものに必要です。<br /><br />-   Office 2010 および Azure RMS<br />-   Office 2010 および Active Directory RMS|
|AD RMS クライアント 1.0 が Azure RMS と連携できるようにするための修正プログラム (KB 2843630)|次のものに必要です。<br /><br />-   Office 2010 および Azure RMS<br />-   Office 2010 および Active Directory RMS|
|AD RMS クライアントおよび RMS 共有アプリケーション|次のものに必要です。<br /><br />-   Office 2016 または Office 2013 および Azure RMS または Active Directory RMS<br />-   Office 2010 および Azure RMS<br />-   Office 2010 および Active Directory RMS<br />-   RMS 共有アプリケーションおよび Office アドインのみ|
|リボン用 Office アドイン|次のものに必要です。<br /><br />-   Office 2016 または Office 2013 および Azure RMS または Active Directory RMS<br />-   Office 2010 および Azure RMS<br />-   Office 2010 および Active Directory RMS<br />-   RMS 共有アプリケーションおよび Office アドインのみ|
|Azure Active Directory Rights Management 準備ツール|次のものに必要です。<br /><br />-   Office 2010 および Azure RMS|
次の手順を使用して、これらのデプロイメント シナリオ用に RMS 共有アプリケーションのデプロイに必要なコマンドを識別します。

-   **Office 2016 または Office 2013 および Azure RMS または Active Directory RMS**

    ユーザーが Office 2016 または Office 2013 を実行しており、組織では Azure RMS または Active Directory RMS を使用していて、ユーザーが Azure RMS または Active Directory RMS を使用している他の組織と共同作業を行っている。

-   **Office 2010 および Azure RMS**

    ユーザーが Office 2010 を実行しており、組織では Azure RMS を使用していて、ユーザーが Azure RMS または Active Directory RMS を使用している他の組織と共同作業を行っている。

-   **Office 2010 および Active Directory RMS**

    ユーザーが Office 2010 を実行しており、組織では AD RMS を使用していて、ユーザーが Azure RMS を使用している他の組織と共同作業を行っている。

-   **RMS 共有アプリケーションおよび Office アドインのみ**

    ユーザーが Office 2016、Office 2013 または Office 2010 を実行しており、組織では AD RMS を使用していて、ユーザーが Azure RMS を使用している他の組織と共同作業を行う必要がない。 このインストールでは、共有アプリケーションと Office アドインのみをインストールできます。

> [!NOTE]
> これらのシナリオにおいて、組織で AD RMS を実行している場合、ユーザーは Azure RMS を使用している他の組織から保護されたコンテンツを受信できますが、Azure RMS を使用している組織のユーザーに保護されたコンテンツを送信することはできません。 ただし、組織が Azure RMS を実行している場合、ユーザーは保護されたコンテンツを他の組織との間で送受信することができます。

各手順のインストールを完了するには、コンピューターを再起動する必要があります。 shutdown /i などのコマンドを使用して、自動再起動を開始できます。

#### Office 2016 または Office 2013 用 RMS 共有アプリケーションおよび Azure RMS または Active Directory RMS をデプロイするには

-   RMS 共有アプリケーションと関連コンポーネントをインストールする各コンピューターで、昇格した特権で次のコマンドを実行します。

    ```
    setup.exe /s
    ```

インストールが成功したかどうかを確認するには、このトピックの「[インストールの成功の確認](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)」を参照してください。

#### Office 2010 用 RMS 共有アプリケーションおよび Azure RMS をデプロイするには

1.  Azure Active Directory Rights Management 準備ツールを実行して組織の証明サービスの URL を取得できるように、Office 365 または Azure Active Directory テナントのグローバル管理者である必要があります。 このツールは、1 台のコンピューターで 1 回のみ実行する必要があります。 RMS 共有アプリケーションを各コンピューターにインストールする場合は、証明サービスの URL を使用します。

    1.  ローカル管理者アカウントを使用して、コンピューターにログインします。

    2.  そのコンピューターで、[Microsoft Online サインイン アシスタントをダウンロードしてインストールします](http://www.microsoft.com/download/details.aspx?id=28177)。

    3.  次のコマンドを実行し、証明サービスの URL を画面に表示します。次に、これをコピーして、この後の手順のために保存します。

        -   Windows 8.1 および Windows 8、64 ビットの場合:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Windows 8.1 および Windows 8、32 ビットの場合:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Windows 7、64 ビットの場合:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > このコマンドでは、Azure の資格情報の入力が求められる場合があります。 コンピューターがドメインに参加していない場合は、入力が求められます。 コンピューターがドメインに参加している場合は、キャッシュされた資格情報をツールで使用できる場合があります。

2.  RMS 共有アプリケーションをインストールする各コンピューターで、昇格した特権で次のコマンドを実行します。

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  RMS 共有アプリケーションをインストールする各コンピューターで、ユーザーは次のコマンドを実行する必要があります (昇格した特権は必要ありません)。 これを行うにはさまざまな方法があります。たとえば、コマンド (電子メール メッセージ内のリンクやヘルプ デスク ポータル上のリンクなど) の実行をユーザーに依頼したり、ログオン スクリプトに追加したりします。

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

インストールが成功したかどうかを確認するには、このトピックの「[インストールの成功の確認](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)」を参照してください。

#### Office 2010 用 RMS 共有アプリケーションおよび Active Directory RMS をデプロイするには

1.  RMS 共有アプリケーションをインストールする各コンピューターで、昇格した特権で次のコマンドを実行します。

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  RMS 共有アプリケーションをインストールする各コンピューターで、ユーザーは次のコマンドを実行する必要があります (昇格した特権は必要ありません)。 これを行うにはさまざまな方法があります。たとえば、コマンド (電子メール メッセージ内のリンクやヘルプ デスク ポータル上のリンクなど) の実行をユーザーに依頼したり、ログオン スクリプトに追加したりします。

    -   Windows 10、Windows 8.1 および Windows 8、64 ビットの場合:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Windows 10、Windows 8.1 および Windows 8、32 ビットの場合:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Windows 7、64 ビットの場合:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

インストールが成功したかどうかを確認するには、このトピックの「[インストールの成功の確認](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)」を参照してください。

#### RMS 共有アプリケーションおよび Office アドインのみをインストールするには

1.  次のコマンドを使用して、AD RMS クライアントと RMS 共有アプリケーションをインストールします。

    -   64 ビット Windows の場合:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   32 ビット Windows の場合:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    例: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  次のコマンドを使用して、Office アドインをインストールします。

    -   64 ビット版の Office の場合:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   32 ビット版の Office の場合:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    例: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

インストールが成功したかどうかを確認するには、このトピックの「[インストールの成功の確認](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)」を参照してください。

### <a name="BKMK_verifyscripted"></a>インストールの成功の確認
インストール ログ ファイルを使用して、インストールの成功を確認することができます。

##### Office 2016 または Office 2013 用 RMS 共有アプリケーションおよび Azure RMS または Active Directory RMS のインストールの成功を確認するには

-   Setup.exe コマンドの成功を確認するには、各コンピューターで、インストール ログ ファイル **RMInstaller.log** を *%temp%\RMS_installer_&lt;guid&gt;* フォルダーで探し、終了コードを確認します。

    インストールが成功した場合、終了コードは 0 となり、それ以外の場合はインストールが失敗したことを示します。

    ログ ファイル名の例:**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

##### Office 2010 用 RMS 共有アプリケーションおよび Azure RMS のインストールの成功を確認するには

1.  Setup.exe コマンドの成功を確認するには、各コンピューターで、インストール ログ ファイル **RMInstaller.log** を *%temp%\RMS_installer_&lt;guid&gt;* フォルダーで探し、終了コードを確認します。

    インストールが成功した場合、終了コードは 0 となり、それ以外の場合はインストールが失敗したことを示します。

    ログ ファイル名の例:**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  RMSSetup.exe コマンドの成功を確認するには、ユーザーが *%localappdata%\microsoft\drm* フォルダーに次のファイルを作成してある必要があります。

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    CLC-&#42;.drm ファイルの例:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

##### Office 2010 用 RMS 共有アプリケーションおよび Active Directory RMS のインストールの成功を確認するには

1.  Setup.exe コマンドの成功を確認するには、各コンピューターで、インストール ログ ファイルを *%temp%\RMS_installer_&lt;guid&gt;* フォルダーで探し、終了コードを確認します。

    インストールが成功した場合、終了コードは 0 となり、それ以外の場合はインストールが失敗したことを示します。

    ログ ファイル名の例:**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  aadrmprep.exe コマンドの成功を確認するには、各コンピューターのインストール ログ ファイルで、**aadrmprep.exe exited with status SUCCESS** というテキストを探します。

    > [!NOTE]
    > 場合によっては、このインストールは 2 回実行され、1 回目に失敗し、2 回目に成功することがあります。

    このツールによるレジストリ変更を手動で確認する場合、変更内容は以下のようになります。

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

##### RMS 共有アプリケーションおよび Office アドインのみのインストールの成功を確認するには

1.  Setup_ipviewer.exe コマンドの成功を確認するには、インストール ログ ファイルで次のテキストを探します。**Installation success or error status:0**

    インストールの成功を示す行の例:

    **MSI (s) (F0:B8) [14:19:57:854]:Product:Active Directory Rights Management Services Client 2.1 -- Installation completed successfully.**

    **MSI (s) (F0:B8) [14:19:57:854]:Windows Installer installed the product. Product Name:Active Directory Rights Management Services Client 2.1. Product Version:1.0.1179.1. Product Language:1033. 製造元:Microsoft Corporation. Installation success or error status:0.**

2.  Office アドインの成功を確認するには、各コンピューターのインストール ログ ファイルで次のテキストを探します。**Installation success or error status:0**

    インストールの成功を示す行の例:

    **MSI (s) (9C:88) [18:49:04:007]:Product:Microsoft RMS Office Addins -- Installation completed successfully.**

    **MSI (s) (9C:88) [18:49:04:007]:Windows Installer installed the product. Product Name:Microsoft RMS Office Addins. Product Version:1.0.7. Product Language:1033. 製造元:Microsoft. Installation success or error status:0.**

### <a name="BKMK_uninstallscripted"></a>アンインストール コマンド
これらのデプロイメントに必要なすべてのインストール コマンドで、アンインストール コマンドがサポートされているわけではありません。 AD RMS クライアントと共有アプリケーションをアンインストールし、Office アドインをアンインストールすることができます。 これらの要素をアンインストールするには、次のコマンドを使用します。

##### AD RMS クライアントおよび RMS 共有アプリケーションをアンインストールするには

-   次のコマンドを使用します。

    -   64 ビット Windows の場合:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   32 ビット Windows の場合:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

##### Office アドインをアンインストールするには

-   次のコマンドを使用します。

    -   64 ビット版の Office の場合:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   32 ビット版の Office の場合:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

### <a name="BKMK_SuppressAutomaticUpdates"></a>自動更新の抑制
既定では、新しいバージョンの RMS 共有アプリケーションがある場合、ユーザーに通知され、ダウンロードを求めるメッセージが表示されます。 次のレジストリを編集すると、この通知が表示されないようにすることができます。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** に移動し、既に存在しない場合は、**RmsSharingApp** という名前の新しいキーを作成します。

2.  **RmsSharingApp** を選択し、新しい DWORD 値の **AllowUpdatePrompt** を作成して、その値を **0** に設定します。

RMS 共有アプリケーションは、WSUS ではサポートされていないため、次の手法を使用して、すべてのユーザーにデプロイする前に RMS 共有アプリケーションの新しいバージョンをテストできます。

1.  すべてのユーザーのコンピューターで、自動更新を抑制するスクリプトを実行します。 管理者が新しいバージョンのテストに使用するコンピューターでは、このスクリプトを実行しないでください。

2.  新しいバージョンが使用可能になったら、管理者はそれをダウンロードしてテストします。

3.  テストが完了し、問題を解決したら、このガイドの自動デプロイメントの手順を使用して、すべてのユーザーに最新バージョンをデプロイします。

### <a name="BKMK_DocumentTracking"></a>Azure RMS のみ:ドキュメント追跡の構成
ドキュメント追跡をサポートする[サブスクリプションがある場合](https://technet.microsoft.com/en-us/dn858608)、組織内のすべてのユーザーに対してドキュメント追跡サイトが既定で有効になっています。ドキュメント追跡では、ユーザーが共有している保護されたドキュメントにアクセスしようとしている人々の電子メール アドレス、これらの人々がアクセスを試みた時刻、およびその場所などの情報が示されます。プライバシーに関する要件により、組織でこの情報の表示が禁止されている場合、[Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) コマンドレットを使用して、ドキュメント追跡サイトへのアクセスを無効にすることができます。サイトへのアクセスは [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) を使用して、いつでも再度有効にすることができます。また、[Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) を使用して、アクセスが現在有効になっているか無効になっているかを確認できます。

 これらのコマンドを使用するには、バージョン **2.3.0.0** 以降の Windows PowerShell 用 Azure RMS モジュールが必要です。インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](https://technet.microsoft.com/library/jj585012.aspx)」を参照してください。

> [!TIP]
> 以前にモジュールをダウンロードしてインストールした場合は、以下を実行してバージョン番号を確認します。`(Get-Module aadrm –ListAvailable).Version`

次の URL はドキュメント追跡で使用されるため、許可する必要があります (たとえば、セキュリティ強化を有効にして Internet Explorer を使用する場合は、信頼済みサイトに追加します):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > この URL は Bing マップ用です。

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### <a name="BKMK_FederatedDomains"></a>AD RMS のみ: 組織内での複数の電子メール ドメインのサポート
AD RMS を使用し、(たとえば、合併や買収の結果) 組織のユーザーが複数の電子メール ドメインを保有している場合は、次のレジストリ編集を行います。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** に移動し、既に存在しない場合は、**RmsSharingApp** という名前の新しいキーを作成します。

2.  **RmsSharingApp** を選択し、**FederatedDomains** という名前の新しい複数文字列値を作成して、組織で使用されるドメインとすべてのサブドメインを追加します。 ワイルドカードはサポートされません。

    例:Coho Vineyard &amp; Winery という会社には、標準の電子メール ドメインとして **cohovineyardandwinery.com** がありますが、合併の結果、**cohowinery.com**、**eastcoast.cohowinery.com**、および **cohovineyard** という電子メール ドメインも使用されています。**FederatedDomains** 値のデータに対して、管理者は **cohowinery.com; eastcoast.cohowinery.com; cohovineyard** を入力します。

このレジストリ変更を行わないと、ユーザーは、組織の他のユーザーによって保護されたコンテンツを使用できなくなる可能性があります。 Azure RMS を使用する場合、このレジストリ編集は必要ありません。

## <a name="BKMK_AdminOverview"></a>Microsoft Rights Management 共有アプリケーションの技術的概要
Microsoft Rights Management 共有アプリケーションは、Microsoft Windows およびその他のプラットフォーム用のオプションのダウンロード可能なアプリケーションであり、次の機能を備えています。

-   1 つのファイルの保護、または複数のファイルや選択したフォルダー内のすべてのファイルの一括保護。

-   任意の種類のファイルの保護の完全なサポートと、一般的に使用されるテキストとイメージ ファイルの種類用の組み込みビューアー。

-   RMS 保護をサポートしていないファイルの一般的な保護。

-   Office Information Rights Management (IRM) を使用して保護されたファイルとの完全な相互運用。

-   SharePoint、FCI、およびサポートされている PDF 作成ツールを使用して保護された PDF ファイルとの完全な相互運用。

Microsoft Rights Management 共有アプリケーションでは、新しい [AD RMS Client 2.1 ランタイム](http://www.microsoft.com/download/details.aspx?id=38396)が使用されます。 Microsoft Rights Management 共有アプリケーションは、AD RMS 2.1 の機能を使用することにより、エンド ユーザーが簡単に保護および使用できるようにします。

RMS の 2013 年 10 月リリースでは、Office 2010 を使用してネイティブにドキュメントを保護し、別の企業のユーザーに送信できます。それらのユーザーは、Azure RMS でドキュメントを使用できます。 さらに、このリリースでは、暗号化モード 2 で AD RMS を使用すると、個人向け RMS を使用して、Azure RMS を使用する別の企業内のユーザーからのコンテンツを利用できます。 暗号化モード 2 の詳細については、「[AD RMS の暗号化モード](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx)」を参照してください。

### <a name="BKMK_LevelsofProtection"></a>保護のレベル - ネイティブとジェネリック
Microsoft Rights Management 共有アプリケーションは、次の表に示すように、2 つの異なるレベルの保護をサポートします。

|保護の種類|ネイティブ|ジェネリック|
|---------|---------|----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および AD RMS をサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類については、ジェネリック保護で、ファイルの種類として .pfile を使用したファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証の両方を含むレベルの保護が提供されます。|
|保護|ファイルは完全に暗号化され、次の方法で保護が適用されます。<br /><br />-   保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br />-   さらに、ファイルが保護されるときにコンテンツの所有者によって設定される使用権限およびポリシーは、コンテンツが IP ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに、完全に適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />-   保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 承認に失敗すると、ファイルは開きません。<br />-   コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br />-   承認済みユーザーがファイルを開き、アクセスする操作の監査ロギングが行われますが、サポートされていないアプリケーションからは使用権限は適用されません。|
|ファイルの種類の既定値|次のファイルの種類の既定の保護レベルを次に示します。<br /><br />-   テキストとイメージ ファイル<br />-   Microsoft Office (Word、Excel、PowerPoint) ファイル<br />-   Portable Document Format (.pdf)<br /><br />詳細については、「[サポートされているファイルの種類とファイル名拡張子](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes)」セクションを参照してください。|これは、完全な保護を通じてサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|
RMS 共有アプリケーションで適用される既定の保護レベルは変更することができます。 既定のレベルをネイティブからジェネリックに、またジェネリックからネイティブに変更することができます。さらに、RMS 共有アプリケーションで保護を適用しないようにすることもできます。 詳細については、このトピックの「[ファイルの既定の保護レベルの変更](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection)」セクションを参照してください。

### <a name="BKMK_SupportFileTypes"></a>サポートされているファイルの種類とファイル名拡張子
Microsoft Rights Management 共有アプリケーションでネイティブにサポートされているファイルの種類を、次の表にリストします。 これらのファイルの種類については、ネイティブの保護が適用され、これらのファイルが読み取り専用になると、元のファイル名拡張子が変更されます。

さらに、RMS 共有アプリケーションで、ユーザーが共有によって保護している Word、Excel、または PowerPoint ファイルをネイティブに保護する場合、この操作により、ファイル名は同じで、ファイル名拡張子が **.ppdf** ¹ である、元のファイルのコピーである 2 番目のファイルが自動的に作成されます。 このバージョンのファイルにより、RMS 共有アプリケーションをインストールする受信者は、常にネイティブ保護が適用されたファイルを開くことができます。

一般的に保護されているファイルの場合、元のファイル名拡張子は常に .pfile に変わります。

> [!WARNING]
> ファイル名拡張子に基づいて検査とアクションを実行するファイアウォール、Web プロキシ、またはセキュリティ ソフトウェアがある場合は、新しいファイル名拡張子をサポートするようにそれらの再構成が必要になる場合があります。

|元のファイル名拡張子|RMS で保護されたファイル名拡張子|
|--------------|----------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jif|.pjif|
|.jt|.pjt|
¹ PDF Rendering Powered by Foxit. Copyright © 2003–2014 by Foxit Corporation.

Microsoft Office 2016、Office 2013 および Office 2010 の Microsoft Rights Management 共有アプリケーションでネイティブにサポートされているファイルの種類を次の表にリストします。 これらのファイルの場合、ファイル名拡張子は、ファイルが RMS で保護された後も変更されません。

|Office でサポートされているファイルの種類|Office でサポートされているファイルの種類|
|----------------------------|----------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="BKMK_ChangeDefaultProtection"></a>ファイルの既定の保護レベルの変更
RMS 共有アプリケーションがファイルを保護する方法は、レジストリを編集して変更することができます。 たとえば、ネイティブ保護をサポートするファイルを、RMS 共有アプリケーションで一般的に保護されるように強制できます。

この操作を行う必要がある理由:

-   すべてのユーザーがモバイル デバイスからファイルを開けるようにするため。

-   ネイティブ保護をサポートするアプリケーションがない場合に、すべてのユーザーがファイルを開けるようにするため。

-   セキュリティ システムがファイル名拡張子に基づいてファイルに対するアクションを実行し、.pfile ファイル名拡張子に対応するように再構成できるが、ネイティブ保護のための複数のファイル名拡張子に対応するように再構成できないようにするため。

同様に、既定ではジェネリック保護が適用されるファイルに、RMS 共有アプリケーションでネイティブ保護を適用するように強制することができます。 これは、社内開発者によって作成された基幹業務アプリケーションや、独立系ソフトウェア ベンダー (ISV) から購入したアプリケーションなど、RMS API をサポートするアプリケーションがあるときに適切な場合があります。

また、RMS 共有アプリケーションでファイルの保護をブロックする (ネイティブ保護やジェネリック保護を適用しない) ように強制することもできます。 たとえば、内容を処理するために特定のファイルを開く必要がある自動化されたアプリケーションまたはサービスがある場合に、これが必要になることがあります。 ファイルの種類の保護をブロックすると、ユーザーは RMS 共有アプリケーションを使用して、そのファイルの種類を持つファイルを保護できなくなります。 ユーザーがこの操作を試みると、管理者が保護できないように設定したことと、ファイルを保護するには操作を取り消す必要があることを示すメッセージが表示されます。

既定ではネイティブ保護が適用されるすべてのファイルにジェネリック保護を適用するように RMS 共有アプリケーションを構成するには、次のレジストリ編集を行います。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**:**&#42;** という名前の新しいキーを作成します。

    この設定は、任意のファイル名拡張子を持つファイルを表します。

2.  新たに追加された **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\ &#42;** キーで、データ値が **Pfile** の **Encryption** という名前の新しい文字列値 (REG_SZ) を作成します。

    この設定により、RMS 共有アプリケーションはジェネリック保護を適用します。

これら 2 つの設定により、RMS 共有アプリケーションは、ファイル名拡張子を持つすべてのファイルにジェネリック保護を適用します。 これが目的である場合、それ以上の構成は必要ありません。 ただし、引き続きネイティブで保護されるように、特定のファイルの種類の例外を定義できます。 そのためには、以下のように、ファイルの種類ごとに追加で 3 つのレジストリ編集を行う必要があります。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**:ファイル名拡張子の名前を持つ新しいキーを追加します (前にピリオドは付けません)。

    たとえば、.docx というファイル名拡張子を持つファイルの場合、**DOCX** という名前のキーを作成します。

2.  新たに追加されたファイルの種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**) で、値が **0** の **AllowPFILEEncryption** という新しい DWORD 値を作成します。

3.  新たに追加されたファイルの種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**) で、値が **Native** の **Encryption** という新しい文字列値を作成します。

これらの設定の結果、RMS 共有アプリケーションでネイティブで保護される .docx というファイル名拡張子を持つファイルを除き、すべてのファイルが一般的に保護されます。

例外として定義するその他のファイルの種類ごとに、これらの 3 つの手順を繰り返します。これらのファイルはネイティブ保護をサポートしており、RMS 共有アプリケーションで一般的に保護しないようにする必要があるためです。

次の値をサポートする **Encryption** 文字列の値を変更することで、他のシナリオで同様のレジストリ編集を行うことができます。

-   **Pfile**:一般保護

-   **Native**:ネイティブ保護

-   **Off**:保護のブロック

## 参照
[Rights Management 共有アプリケーション ユーザー ガイド](../Topic/Rights_Management_sharing_application_user_guide.md)


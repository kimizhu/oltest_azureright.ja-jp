---
description: na
keywords: na
pagetitle: Logging and Analyzing Azure Rights Management Usage
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
---
# Azure Rights Management の利用状況をログに記録して分析する
このトピックでは、Azure Rights Management (Azure RMS) で使用状況ログを使用する方法について説明します。 Azure Rights Management サービスは、組織のために処理したすべての要求のログを記録します。このログには、組織内のユーザーからの要求、Rights Management 管理者が実行した操作、Azure Rights Management デプロイをサポートするために Microsoft オペレーターが実行した操作などが含まれます。

これらの Azure Rights Management ログを使用すると、次のビジネス シナリオをサポートできます。

-   ビジネス情報を分析する

    Azure Rights Management は、W3C 拡張ログ形式のログを指定された Azure ストレージ アカウントに書き込みます。 これらのログを選択したリポジトリ (データベース、オンライン分析処理 (OLAP) システム、MapReduce システムなど) に転送することによって、情報を分析してレポートを生成できます。 たとえば、RMS で保護されているデータにだれがアクセスしているかを識別できます。 RMS で保護されているどのデータにアクセスしているか、どのデバイスから、およびどの場所からアクセスしているかを特定できます。 また、保護されているコンテンツを正常に読むことができたかどうかを調べることができます。 さらに、保護されている重要なドキュメントを読んだユーザーを識別することもできます。

-   不正使用を監視する

    Azure Rights Management ログ情報はほぼリアルタイムに提供されるため、組織での Rights Management の使用状況を途切れなく監視できます。 ログの 99.9% は、RMS が操作を実行してから 15 分以内に提供されます。

    たとえば、RMS で保護されているデータを標準勤務時間外に読むユーザーの数が突然増加した場合に警告を受け取りたい場合があります。この場合、悪意のあるユーザーが競合他社に売り渡すために情報を収集している可能性があります。 また、明らかに同じユーザーが短時間に 2 つの異なる IP アドレスからデータにアクセスした場合、これはユーザー アカウントが侵害されたことを示している可能性があります。

-   科学捜査上の分析を実行する

    情報漏えいが発生した場合、特定のドキュメントにだれが最近アクセスしたか、および疑わしいユーザーが最近どの情報にアクセスしたかをたずねられる可能性があります。 Azure Rights Management およびログを使用すれば、このような質問に答えることができます。保護されているコンテンツを使用するユーザーが Azure Rights Management で保護されているドキュメントおよび画像を開くには、常に Rights Management ライセンスを取得する必要があるためです。これは、ファイルがメールで転送されたり、USB ドライブなどのストレージ デバイスにコピーされたりした場合も同様です。 このため、Azure Rights Management を使用してデータを保護していれば、Azure Rights Management ログを科学捜査上の分析のための最終的な情報源として活用できます。

> [!NOTE]
> Azure Rights Management の管理タスクのログ記録だけに関心があり、Rights Management の利用状況追跡は望まない場合は、Azure Rights Management の [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) Windows PowerShell コマンドレットを使用できます。
> 
> **RMS の利用状況**、**最もアクティブな RMS ユーザー**、**RMS デバイスの使用状況**、**RMS で有効なアプリケーションの使用状況**など、概要レベルの使用状況レポートについて Azure クラシック ポータルを使用することもできます。 Azure クラシック ポータルからこれらのレポートにアクセスするには、**[Active Directory]** をクリックしてディレクトリを選択して開き、**[レポート]** をクリックします。

次のセクションでは、Azure Rights Management の使用状況ログの詳細について説明します。

-   [Azure Rights Management の使用状況ログを有効にする方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_EnableRMSLogging)

-   [Azure Rights Management の使用状況ログにアクセスして使用する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs)

-   [Azure Rights Management のログ ストレージを管理する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_ManageStorage)

-   [Azure Rights Management の使用状況ログへのアクセスを委任する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate)

-   [Azure Rights Management の使用状況ログを解釈する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret)

-   [Windows PowerShell の参照情報](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_PowerShell)

## <a name="BKMK_EnableRMSLogging"></a>Azure Rights Management の使用状況ログを有効にする方法
Azure Rights Management の使用状況ログは既定では有効にされていないため、使用する場合は特定の手順を実行する必要があります。 Azure Rights Management の使用状況ログを使用する場合でも、Rights Management の機能に変更はなく、ログ プロセス自体も無料です。 ただし、RMS ログ用に Azure ストレージ アカウントが必要となり、このストレージには料金がかかります。

始める前に、Azure Rights Management の使用状況ログを使用するための次の前提条件を満たしていることを確認してください。

|要件|詳細情報|
|------|--------|
|Azure Rights Management を含む IT 管理のサブスクリプション|所属組織によって管理されている Microsoft Azure Rights Management サブスクリプションが必要です。 個人向け RMS を使用する組織は Azure Rights Management の使用状況ログを使用できません。<br /><br />個人向け RMS を使用しているユーザーが組織に存在する場合、Azure Rights Management の使用状況ログ記録を使用するには、個人向け RMS を Microsoft Azure Rights Management サブスクリプションに移行する必要があります。<br /><br />Azure RMS に含まれるサブスクリプションの詳細については、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」トピックの「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションを参照してください。<br /><br />個人用 RMS の詳細については、「[個人用 RMS と Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)」を参照してください。|
|を保有する管理者が|Azure のサブスクリプション、および Azure 上に Azure Rights Management ログ用の十分なストレージが必要です。|
|Azure Rights Management 用 Windows PowerShell|Azure Rights Management 用 Windows PowerShell モジュールのダウンロードとインストールが完了していない場合は実行します。 Windows PowerShell コマンドレットは、Azure Rights Management の使用状況ログを構成および管理するために使用します。<br /><br />詳細については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。|
Azure Rights Management の使用状況ログを有効にするには、次の手順に従います。この手順では、まず Azure ストレージ アカウントを作成し、次にそのストレージ アカウントを Rights Management ログ用として使用するように Azure を構成します。

> [!NOTE]
> この手順は、Azure アカウントを持っていることを前提としています。 Azure Rights Management の使用状況ログでは個人用アカウントがサポートされていますが、ベスト プラクティスとして職場または学校のアカウントを使用してください。 また、Rights Management ログ専用のストレージ アカウントを作成することをお勧めします。 ストレージ アクセス キーは Azure Rights Management と共有し、また他のユーザーがログ ファイルを使用する場合はそれらのユーザーと共有する必要があります。
> 
> Azure ストレージの詳細については、「[Azure ストレージのドキュメント](http://azure.microsoft.com/documentation/services/storage/)」を参照してください。

#### ストレージ アカウントを作成し、Azure Rights Management の使用状況ログを有効にする方法

1.  [Azure ポータル](https://portal.azure.com/)にサインインします。

2.  [ハブ] メニューで、**[新規]**、**[データ + ストレージ]**、**[ストレージ アカウント]** の順に選択します。

    > [!TIP]
    > このオプションが表示されない場合は、Rights Management のサブスクリプションだけでなく、Azure サブスクリプションがあることを確認してください。

3.  **[クラシック]** の既定の配置モデルのまま、**[作成]** をクリックします。

    ストレージ アカウントの名前を指定し、必要に応じて、**[価格レベル]**、**[リソース グループ]**、**[サブスクリプション]**、**[ダッシュボードにピン留めする]** の選択されているオプションを変更します。 次に、**[作成]** をクリックします。**"ストレージ アカウントの作成"** アクティビティが完了するのを待ちます。

4.  新しく作成されたストレージ アカウントをクリックし、**[設定]** をクリックします。

5.  **[設定]** ブレードで **[キー]** アイコンをクリックします。

6.  **[キーの管理]** ブレードで **[プライマリ アクセス キー]** の値をコピーし、ブレードを閉じます。

7.  [**管理者として実行**] オプションを使用して Windows PowerShell を起動します。[Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) コマンドを実行して Azure Rights Management サービスに接続します。

    ```
    Connect-AadrmService
    ```

8.  [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) コマンドを使用して Azure Rights Management の使用状況ログの保管場所を指定します。*&lt;Access_Key&gt;* は手順 6. でコピーしたプライマリ アクセス キーに、*&lt;StorageAccount&gt;* は手順 3. で作成したストレージ アカウントにそれぞれ置き換えます。

    ```
    $accesskey = convertto-securestring -asplaintext -force –string <Access_Key> Set-AadrmUsageLogStorageAccount -AccessKey $accesskey -StorageAccount <StorageAccount>
    ```

9. [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx) コマンドを使用し、Azure Rights Management の使用状況ログを有効にします。

    ```
    Enable-AadrmUsageLogFeature
    ```
    次のメッセージが表示されます。**The usage log feature is enabled for the Rights management service. (Rights management service の利用状況ログ機能が有効です。)**

使用状況ログが有効になったので、Azure Rights Management は組織のすべての操作をログに記録し始め、この情報をストレージ アカウントに保存します。 この時点ではログ情報はまだ使用可能ではありません。

ストレージ アカウントの作成方法の詳細については、Azure ドキュメントで「[Azure ストレージ アカウントについて](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」の「[ストレージ アカウントの作成](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」セクションを参照してください。

## <a name="BKMK_AccesAndUseLogs"></a>Azure Rights Management の使用状況ログにアクセスして使用する方法
Azure Rights Management は、ログを Azure ストレージ アカウントに一連の BLOB として書き込みます。 各 BLOB には、W3C 拡張ログ形式の 1 つ以上のログ レコードが含まれています。 BLOB の名前は、作成された順序を表す数字です。 ログの内容および作成の詳細については、このドキュメントの後半の「[Azure Rights Management の使用状況ログを解釈する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret)」セクションで説明します。

Azure Rights Management 操作の実行後、ログがストレージ アカウントに書き込まれるまで若干時間がかかります。 ほとんどのログは 15 分以内に表示されます。

Azure Rights Management の使用状況ログ用に作成したストレージ アカウントはメールボックスに似ており、ストレージ アカウントから直接ログを読むことができますが、これは最適な使い方ではありません。 最高のパフォーマンスを引き出し、コストを削減するために、ログをローカル ストレージ (ローカル フォルダー、データベース、MapReduce リポジトリなど) にダウンロードすることをお勧めします。

使用状況ログは次の 2 つの方法でダウンロードできます。

-   Windows PowerShell コマンドレット [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx) を使用する。

    これは使用状況ログにアクセスするための最も単純な方法です。 このコマンドレットによって、ログがコンピューターにダウンロードされます。各 BLOB は指定した場所にファイルとしてダウンロードされます。

-   [Azure Storage SDK](http://www.windowsazure.com/en-us/develop/net/) を使用し、ログをダウンロードするためのカスタム アプリケーションを作成します。

    カスタム アプリケーションは、Get-AadrmUsageLogs コマンドレットより高い柔軟性を備えています。 たとえば、Azure Rights Management 管理者の資格情報の使用が禁止されている他のユーザーまたはプロセスにログのダウンロードを委任できます。 また、ログをリアル タイムにポーリングして誤使用がないかどうかを監視できます。

#### PowerShell を使用して使用状況ログをダウンロードするには

-   [**管理者として実行**] オプションを使用して Windows PowerShell を起動し、**Get-AadrmUsageLog –Path &lt;location&gt;** を実行します。 たとえば、E ドライブに **logs** という名前のフォルダーを作成すると、次のようになります。

    -   使用可能なログを E:\logs フォルダーにダウンロードするには: `Get-AadrmUsageLog -Path "e:\logs"`

    -   特定の範囲の BLOB をダウンロードするには: `Get-AadrmUsageLog –Path "e:\logs" –FromCounter 1024 –ToCounter 2047`

これらのコマンドレットを実行すると、Windows PowerShell には最後にダウンロードされた BLOB の名前が表示されます。 この名前を変数に代入することにより、Get-AadrmUsageLog をループまたはスケジュール ジョブとして実行して、各ジョブで増分ログのみをダウンロードできます。

例:

**PS C:\&gt; $LastBlobName = Get-AadrmUsageLog –Path "e:\logs"**

**1527**

**PS C:\&gt; $LastBlobName**

**1527**

> [!TIP]
> [Microsoft のログ パーサー](http://www.microsoft.com/download/details.aspx?id=24659)を利用し、ダウンロードしたすべてのログ ファイルを CSV 形式で集計できます。このログ パーサーは既知のさまざまなログ形式間で変換するためのツールです。 また、このツールを使用すると、データを SYSLOG 形式に変換したり、データベースにインポートしたりできます。 このツールをインストールしたら、**LogParser.exe /?** を実行してこのツールのヘルプおよび使い方を表示します。 たとえば、次のコマンドを実行すると、すべての情報を .log ファイル形式 **logparser –i:w3c –o:csv “SELECT &#42; INTO AllLogs.csv FROM &#42;.log”** にインポートできます。

使用状況ログは中断および再開できます。 ログを中断した場合でも、Azure Rights Management はストレージ アカウント情報を保持するため、ログを簡単に再開できます。

#### 使用状況ログを中断および再開するには

-   ログを中断するには、次のコマンドレットを使用します:[Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   ログを再開するには、次のコマンドレットを使用します:[Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   ログが有効になっているかどうかを確認するには、次のコマンドレットを使用します:[Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

    値が **True** の場合は Azure Rights Management の使用状況ログが有効になっており、**False** の場合は使用状況ログは無効になっています。

## <a name="BKMK_ManageStorage"></a>Azure Rights Management のログ ストレージを管理する方法
Azure Rights Management ログを保管するために使用するストレージは有料です。

Azure Rights Management では、使用状況ログ ファイルは自動的には管理されません。 ユーザーが操作しない限り、ログはストレージ アカウントに保存されたままになります。 しかし、ダウンロード後にログを削除することによって、容量を節約して記憶域コストを削減できます。 また、削除するファイルを選択することもできます。 1 つの例外を除き、Azure Rights Management はこれらのログ ファイルを使用しません。このため、ログ ファイルをいつ削除できるかについての制約はありません。

削除 (または変更) してはいけないファイルは **rms-metadata** コンテナーにある指定**メタデータ**です。 Azure Rights Management はこの BLOB に基づいて最後に使用した BLOB 番号を追跡します。 このファイルが削除された場合、Azure Rights Management はログ用に新しいコンテナーを作成し、BLOB 番号を 1 から開始します。Get-AadrmUsageLog コマンドレットによる以降のすべてのダウンロードでは、この新しいコンテナーを使用してログ ファイルがダウンロードされます。 この結果、元のコンテナー内のログは保持されますが、孤立します。 孤立したこれらのログをダウンロードする唯一の方法は、Azure ストレージ SDK を使用することです。

> [!TIP]
> Azure Rights Management のログ ストレージを自分で管理する代わりに、ストレージ アカウント名およびアクセス キーを共有することでこの管理機能を別の会社に委任できます。 詳細については、このトピックの後半の「[Azure Rights Management の使用状況ログへのアクセスを委任する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate)」セクションをご覧ください。

場合によっては、ストレージ アクセス キーを再生成する必要が生じます。 例:

-   Azure Rights Management の使用状況ログを管理する会社を変更する場合

-   ストレージ アクセス キーが侵害された疑いがある場合

このようなケースが発生した場合は、セカンダリ アクセス キーを使用してサービスの継続性を確保します (それまでプライマリ アクセス キーを使用していたことが前提となります)。 前に使用していなかったセカンダリ アクセス キーを再生成したら、その新しいキーを使用するように Azure Rights Management を構成します。 次の手順に従ってセカンダリ アクセス キーを再生成し、そのキーを使用するように Azure Rights Management を構成します。

#### セカンダリ アクセス キーを再生成するには

1.  [Azure ポータル](https://portal.azure.com/)にサインインします。

2.  **[すべてのリソース]** をクリックし、テキスト ボックスにストレージ名を入力してストレージを検索します。

3.  ストレージを選択し、**[設定]** をクリックします。

4.  **[キー]** アイコンをクリックします。

5.  **[キーの管理]** セクションで **[セカンダリ キーの再生成]** をクリックし、セカンダリ アクセス キーを再生成することを確認するために [はい] をクリックします。新しいセカンダリ アクセス キーをクリップボードにコピーします。

    Azure ポータルを閉じないでください。

6.  **[管理者として実行]** オプションを使用して Windows PowerShell を起動し、[Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) コマンドレットを使用してこの新しいアクセス キーを使用するように Azure Rights Management を構成します。この場合、*&lt;StorageAccount&gt;* はストレージ アカウントの名前に、*&lt;Access_Key&gt;* は前の手順でコピーした再生成されたセカンダリ アクセス キーにそれぞれ置き換えます。

    ```
    Set-AadrmUsageLogStorageAccount -StorageAccount <StorageAccount>-AccessKey <Access_Key>
    ```
    > [!WARNING]
    > このコマンドを実行するときに別のストレージ アカウントに切り替えることができますが、この操作を行うとそれまでのログが孤立し、Set-AadrmUsageLogStorageAccount コマンドレットまたは同種の管理コマンドおよび管理機能からアクセスできなくなります。

7.  Azure ポータルに戻り、**[キーの管理]** セクションでプライマリ アクセス キーを再生成します。

ストレージ アクセス キーの管理方法の詳細については、Azure ドキュメントで「[Azure ストレージ アカウントについて](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」の「[ストレージ アクセス キーの管理](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」セクションを参照してください。

## <a name="BKMK_Delegate"></a>Azure Rights Management の使用状況ログへのアクセスを委任する方法
ストレージ アカウント名およびアクセス キーを共有することによって、RMS ログへのアクセスを委任できます。 たとえば、別の管理者ユーザー、同じ組織内の開発者、または独立系ソフトウェア ベンダー (ISV) にアクセスを委任できます。 こうしたユーザーは RMS 管理者の資格情報を持っていないため、Get-AardrmUsageLog コマンドレットを使用して RMS ログをダウンロードできません。 代わりに、Windows ストレージ SDK を使用してログをダウンロードする必要があります。 別の方法として、Azure ストレージからログを直接読み取るアプリケーションを作成することもできます。

ストレージ アカウントが RMS ログ専用であれば、この方法で安全にストレージ アカウント名およびアクセス キーを共有できます。 他のユーザーが自分のアクセス キーを持っていても、それらのユーザーはそのキーを使用して他のストレージ アカウントにアクセスすることも、RMS テナント アカウントを使用することもできません。

## <a name="BKMK_Interpret"></a>Azure Rights Management の使用状況ログを解釈する方法
Azure Rights Management の使用状況ログを解釈するには、次の情報を活用してください。

### ストレージ アカウントのレイアウト
Azure Rights Management は、初めてストレージ アカウントにログを書き込むときに、次の 2 つのコンテナーを作成します。

-   **Rms-metadata**:このコンテナーは、Azure Rights Management 用に予約されています。 このコンテナーは変更または削除しないでください。

-   **Rms-logs-&lt;guid&gt;**:Azure Rights Management は、このコンテナーにログを作成して保存します。 収集されたログ情報が不要になった場合は、このコンテナー内のファイルであればすべて安全に削除できます。

時間の経過に伴い、Azure Rights Management により新しい **Rms-logs-&lt;guid&gt;** コンテナーが作成される場合があります。 たとえば、**Rms-metadata** コンテナーが破損したり、誤って削除されたりした場合、Azure Rights Management によりその内容がリセットされ、以降のログ用に新しい **Rms-logs-&lt;guid&gt;** コンテナーが作成されます。 古いコンテナーにある古いログは削除されませんが、孤立化します。

### ログ シーケンス
Azure Rights Management は、ログを一連の BLOB として書き込みます。 各 BLOB には、W3C ログ形式の 1 つ以上のログ レコードが含まれています。

各 BLOB の名前は番号です。 各ログ コンテナー内では、最初の BLOB には 000000001 という名前が付けられます。 各 BLOB には、作成された順序で順番に名前が付けられます。 各 BLOB には、1 つ以上のログ レコードが含まれています。 各ログ レコードには、対応する要求が Azure Rights Management によっていつ処理されたかを示す UTC タイム スタンプが付けられます。

> [!IMPORTANT]
> Azure Rights Management ログ システムは、ログを厳密な時間順ではなく、迅速に提供するように最適化されています。 したがって、BLOB の順序およびログ レコードの順序は時間順ではない場合があります。 BLOB の名前が通し番号である理由は、それらを効率的に増分ダウンロードできるようにするためであり、他に理由はありません。
> 
> 次に、発生する可能性があるログ シーケンスの例を 2 つ示します。
> 
> -   BLOB 000000004 内のログ レコードの時間が、BLOB 000000003 内のログ レコードと重複する場合があります。 極端な場合、BLOB 000000004 内のすべてのログ レコードが BLOB 000000003 内のすべてのログ レコードより前に生成されたものである場合があります。
> -   BLOB の 2 番目のログ レコードが、最初のログ レコードより前に生成されたにもかかわず逆の順序でストレージに書き込まれる場合があります。

Azure Rights Management の使用状況ログを分析する前に、ログをダウンロードし、リポジトリにインポートして、ログをそのタイムスタンプに基づいて並べ替えることをお勧めします。 ログのダウンロードの詳細については、このトピックの「[Azure Rights Management の使用状況ログにアクセスして使用する方法](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs)」セクションを参照してください。

ログは必ずしも時間順ではありませんが、そのほとんどは要求から 15 分以内に書き込まれます。このため、タイムスタンプを使用して必要なログを識別する場合は、対象となる時間に 15 分を加算します。 その後、それらのログをダウンロードします。 このようにすることで、ほとんどすべてのログを取得できることになります。

また、各ログ レコードのタイムスタンプは要求を処理する Azure Rights Management サービスのローカル時間であることに注意してください。 Azure Rights Management は複数のデータ センターにまたがる複数のサーバー上で実行されるため、タイムスタンプで並べ替えられたログであっても、それらが順序どおりではないように見える場合があります。 しかし、その差はわずかであり、通常 1 分以内です。 ほとんどの場合、ログの分析でこれが問題になることはありません。

### BLOB の形式
各 BLOB は、W3C 拡張ログ形式です。 BLOB は、次の 2 行で始まります。

**#Software:RMS**

**#Version:1.1**

最初の行は、これらが Azure Rights Management ログであることを示します。 2 番目の行は、BLOB の残りの部分がバージョン 1.1 の仕様に準拠していることを示します。 これらのログを解析するアプリケーションでは、上の 2 つの行を検証してから BLOB の残りを解析することをお勧めします。

3 番目の行には、タブで区切られたフィールド名が列挙されます。

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

後続の各行はログ レコードです。 フィールド値の順序は前の行と同じで、タブで区切られます。 フィールドを解釈するには、次の表を参照してください。

|フィールド名|W3C データ型|説明|値の例|
|----------|------------|------|-------|
|date|日付|要求が処理された UTC 日付。<br /><br />ソースは、要求にサービスを提供したサーバーのローカル クロックです。|2013-06-25|
|time|時刻|要求が処理された UTC 時間 (24 時間形式)。<br /><br />ソースは、要求にサービスを提供したサーバーのローカル クロックです。|21:59:28|
|row-id|テキスト|このログ レコードの固有 GUID。<br /><br />この値は、ログを別の形式に集約またはコピーするときに役立ちます。|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|名前|要求された RMS API の名前。|AcquireLicense|
|user-id|文字列|要求を行ったユーザー。<br /><br />この値は単一引用符で囲まれます。 要求の種類が匿名の場合、値は ”です。|‘joe@contoso.com’|
|結果|文字列|要求が正常に処理された場合は‘Success’ です。<br /><br />要求が失敗した場合はエラーの種類が単一引用符で囲まれて示されます。|‘Success’|
|correlation-id|テキスト|特定の要求に対する RMS クライアント ログとサーバー ログ間で共通の GUID。<br /><br />この値はクライアントの問題を解決するために役立ちます。|cab52088-8925-4371-be34-4b71a3112356|
|content-id|テキスト|保護されたコンテンツ (ドキュメントなど) を示す、波かっこで囲まれた GUID。<br /><br />このフィールドには request-type が AcquireLicense の場合にのみ値が含まれ、それ以外の場合は空白になります。|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|文字列|ドキュメントの所有者の電子メール アドレス。|alice@contoso.com|
|issuer|文字列|ドキュメントの発行者の電子メール アドレス。|alice@contoso.com (または) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Template-id|文字列|ドキュメントを保護するために使用されるテンプレートの ID。|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|File-name|文字列|保護されたドキュメントのファイル名。|TopSecretDocument.docx|
|Date-published|日付|ドキュメントが保護された日付。|2015-10-15T21:37:00|
|c-info|文字列|要求を行っているクライアント プラットフォームに関する情報。<br /><br />この文字列はアプリケーション (オペレーティング システム、ブラウザーなど) によって異なります。|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|住所|要求を行ったクライアントの IP アドレス。|64.51.202.144|

#### user-id フィールドの例外
通常、user-id フィールドは要求を行ったユーザーを示しますが、値が実際のユーザーにマップされない例外が 2 つあります。

-   値 **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**。

    これは、Office 365 サービス (Exchange Online や Sharepoint Online など) が要求を行っていることを示します。 この文字列で、*&lt;YourTenantID&gt;* はテナントの GUID、*&lt;region&gt;* はテナントが登録されている地域です。 たとえば、**na** は北アメリカを表し、**eu** はヨーロッパを表し、**ap** はアジアを表します。

-   RMS コネクタを使用している場合

    このコネクタから要求は、RMS コネクタのインストール時に RMS が自動的に生成したサービス プリンシパル名でログに記録されます。

#### 一般的な要求の種類
Azure Rights Management には多くの要求の種類がありますが、次の表に一般的に使用される要求の種類を示します。

|要求の種類|説明|
|---------|------|
|AcquireLicense|Windows ベースのマシンのクライアントが RMS で保護されているコンテンツのライセンスを要求しています。|
|AcquirePreLicense|ユーザーに代わってクライアントが、RMS で保護されているコンテンツのライセンスを要求しています。|
|AcquireTemplates|テンプレート ID に基づいてテンプレートを取得するための呼び出しが行われました。|
|AcquireTemplateInformation|サービスからテンプレートの ID を取得するための呼び出しが行われました。|
|AddTemplate|Azure クラシック ポータルから、テンプレートを追加するための呼び出しが行われます。|
|BECreateEndUserLicenseV1|モバイル デバイスから、エンド ユーザー ライセンスを作成するための呼び出しが行われます。|
|BEGetAllTemplatesV1|モバイル デバイス (バックエンド) から、すべてのテンプレートを取得するための呼び出しが行われます。|
|Certify|クライアントが保護のために内容を証明しています。|
|Decrypt|クライアントが RMS で保護されているコンテンツを復号化しようとしています。|
|DeleteTemplateById|Azure クラシック ポータルから、テンプレート ID でテンプレートを削除するための呼び出しが行われます。|
|ExportTemplateById|Azure クラシック ポータルから、テンプレート ID に基づいてテンプレートをエクスポートするための呼び出しが行われます。|
|FECreateEndUserLicenseV1|AcquireLicense 要求と同じですが、要求元はモバイル デバイスです。|
|FECreatePublishingLicenseV1|Certify および GetClientLicensorCert の組み合わせと同じですが、要求元はモバイル クライアントです。|
|FEGetAllTemplates|モバイル デバイス (フロントエンド) から、テンプレートを取得するための呼び出しが行われます。|
|GetAllTemplates|Azure クラシック ポータルから、すべてのテンプレートを取得するための呼び出しが行われます。|
|GetClientLicensorCert|クライアントは Windows ベースのコンピューターから発行元証明書 (後でコンテンツの保護に使用する) を要求しています。|
|GetConfiguration|Azure RMS テナントの構成を取得するために、Azure PowerShell コマンドレットが呼ばれます。|
|GetConnectorAuthorizations|RMS コネクタから、構成をクラウドから取得するための呼び出しが行われます。|
|GetTenantFunctionalState|Azure クラシック ポータルが、Azure RMS がアクティブかどうかを調べています。|
|GetTemplateById|Azure クラシック ポータルから、テンプレート ID を指定してテンプレートを取得するための呼び出しが行われます。|
|ExportTemplateById|Azure クラシック ポータルから、テンプレート ID を指定してテンプレートをエクスポートするための呼び出しが行われています。|
|FindServiceLocationsForUser|Certify または AcquireLicense の呼び出しに使用される URL を照会するための呼び出しが行われます。|
|ImportTemplate|Azure クラシック ポータルから、テンプレートをインポートするための呼び出しが行われます。|
|ServerCertify|RMS 対応クライアント (SharePoint など) から、サーバーを認証するための呼び出しが行われます。|
|SetUsageLogFeatureState|使用状況ログを有効にするための呼び出しが行われます。|
|SetUsageLogStorageAccount|Azure RMS ログの場所を指定するための呼び出しが行われます。|
|SignDigest|署名にキーが使用される場合に呼び出しが行われます。 通常、これは AcquireLicence (または FECreateEndUserLicenseV1)、Certify、GetClientLicensorCert (または FECreatePublishingLicenseV1) ごとに 1 回呼び出されます。|
|UpdateTemplate|Azure クラシック ポータルから、既存のテンプレートを更新するための呼び出しが行われます。|

## <a name="BKMK_PowerShell"></a>Windows PowerShell の参照情報
Azure Rights Management の使用状況ログを構成して使用するには、次の Windows PowerShell コマンドレットを使用します。

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Azure Rights Management 用 Windows PowerShell コマンドレットの使用の詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)」を参照してください。

## 参照
[Azure Rights Management を使用する](../Topic/Using_Azure_Rights_Management.md)


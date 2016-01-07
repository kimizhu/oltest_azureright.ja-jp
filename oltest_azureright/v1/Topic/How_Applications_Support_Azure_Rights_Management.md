---
description: na
keywords: na
pagetitle: How Applications Support Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
---
# アプリケーションで Azure Rights Management をサポートする方法
次の情報は、エンドユーザー アプリケーション (Office アプリケーション、Word、Excel、PowerPoint、Outlook など) およびサービス (Exchange、SharePoint など) が Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を使用して、組織のデータの保護を可能にする方法を理解する場合に役立ちます。

-   [Windows およびモバイル プラットフォーム用の RMS 共有アプリケーション](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharingAppIntro)

-   [Office アプリケーション:Word、Excel、PowerPoint、Outlook](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_OfficeAppsIntro)

    -   [Exchange Online と Exchange Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_ExchangeIntro)

    -   [SharePoint Online と SharePoint Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharePointIntro)

-   [Windows Server を実行するファイル サーバーとファイル分類インフラストラクチャ (FCI) の使用](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_FCIIntro)

-   [RMS API をサポートするその他のアプリケーション](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_APIAppsIntro)

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) によってサポートされるアプリケーションとバージョンを確認するには、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」を参照してください。

場合によっては、構成するポリシーに従って情報保護が自動的に適用されます。 たとえば、SharePoint ライブラリ、分類されたファイル、Exchange トランスポート ルールなどがこれに該当します。 それ以外の場合は、ユーザーが、テンプレートを選択するか特定のオプションを選択して、アプリケーションから情報保護を自分で適用する必要があります。 たとえば、ユーザーが電子メールでファイルを共有する場合や、選択したユーザーまたは組織外のユーザーにアクセスや使用を制限することでファイルをその場で保護する場合などがこれに該当します。

テンプレートを使用すると、ユーザー (およびポリシーを構成する管理者) が、簡単に正しいレベルの保護を適用し、組織内のユーザーにアクセスを制限することができます。[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] には、2 つの既定のテンプレートが付属していますが、カスタム テンプレートを作成すると、個別のオプションの指定が必要な回数を減らすことができます。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md)」を参照してください。

ユーザーが情報保護を自分で適用する必要がある場合は、必ずユーザーに指示を与え、適用の方法とタイミングに関するガイダンスを提供してください。 ユーザーが使用するアプリケーションとバージョンおよびそれらの使用方法に適した指示を提供し、ビジネスに適した方法とタイミングで情報保護を適用するためのガイダンスを提供する必要があります。 詳細については、「[ユーザーに Azure Rights Management でファイルを保護するためのヘルプを提供する](../Topic/Helping_Users_to_Protect_Files_by_Using_Azure_Rights_Management.md)」を参照してください。

Azure RMS のためにこれらのアプリケーションを構成する方法については、「[Azure Rights Management 用にアプリケーションを構成する](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)」を参照してください。

> [!TIP]
> Azure RMS を使用するアプリケーションの例とスクリーンショットについては、「[Azure Active Directory Rights Management の概要](../Topic/What_is_Azure_Rights_Management_.md)」の「[Azure RMS の動作:管理者およびユーザーに対する表示](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures)」セクションを参照してください。

## <a name="BKMK_SharingAppIntro"></a>Windows およびモバイル プラットフォーム用の RMS 共有アプリケーション
RMS 共有アプリケーションは、無料でダウンロードできるアプリケーションであり、Office 2010 のサポートには必須で、Windows コンピューター、Mac コンピューター、モバイル デバイスにも推奨されます。 利点の 1 つとして、[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] をネイティブでサポートしないアプリケーションやファイルの汎用的な保護を適用できることが挙げられます。つまり、すべてのファイルを保護できるということです。 各種の保護レベルの詳細については、「[Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003.aspx)」の「[保護のレベル – ネイティブと汎用](http://technet.microsoft.com/library/dn339003.aspx)」セクションを参照してください。

ユーザーが RMS 共有アプリケーションを使用してファイルを保護すると、ユーザーが保護したドキュメントを追跡したり、必要に応じてそれらへのアクセスを取り消したりすることもできます。 これを行うには、[ドキュメント追跡サイト](http://go.microsoft.com/fwlink/?LinkId=529562)を使用します。

Windows コンピューターの場合、RMS 共有アプリケーションは、ユーザーが既に使用しているアプリケーションに既に統合されていて機能を拡張しています。

-   Word、Excel、PowerPoint、および Outlook 用の Office アドインのインストール。 このアドオンにより、[**保護された共有**] ボタンがリボンに表示され、このボタンをクリックすると、電子メールで送信されるファイルの保護の設定に最もよく使用される、使いやすいダイアログ ボックスが開きます。 また、このボタンを利用するとドキュメント追跡サイトに簡単にアクセスできます。

-   エクスプローラーの新しい右クリック オプション。 このオプションにより、[**インプレースの保護**] オプションが表示され、このボタンをクリックすると、ディスクに保存されているファイルの保護の設定に最もよく使用される、使いやすいダイアログ ボックスが開きます。

-   [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] によって保護されているファイルを開くためのビューアー。 このビューアーは、保護されたファイルを開くことができるアプリケーションが他にインストールされていない場合に自動的に起動します。

-   Office 2010 のバックエンド構成により、このスイートの Word、Excel、PowerPoint、および Outlook が [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] とシームレスに連携できるようになります。

Windows 用の RMS 共有アプリケーションは、[Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) ページを使用して 1 つのコンピューターにダウンロードしてインストールできますが、サイレント インストールおよびカスタム構成のためのエンタープライズ デプロイもサポートされています。 詳細については、次のリソースを参照してください。

-   [Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003.aspx)

-   [Rights Management 共有アプリケーション ユーザー ガイド](http://technet.microsoft.com/library/dn339006.aspx)

モバイル デバイス用の RMS 共有アプリケーションは、iPad、iPhone、Android、Windows Phone、Windows RT などの最も一般的に使用されているモバイル デバイスをサポートします。 ユーザーは、関連するストアからこのアプリをダウンロードできます。[Microsoft Rights Management ページ](http://go.microsoft.com/fwlink/?LinkId=303970)には、それらのリンクがあります。

## <a name="BKMK_OfficeAppsIntro"></a>Office アプリケーション:Word、Excel、PowerPoint、Outlook
これらのアプリケーションでは、Information Rights Management (IRM) を使用することで Rights Management がネイティブでサポートされ、ユーザーは保存済みドキュメントまたは送信される電子メール メッセージに保護を適用できます。 ユーザーは、テンプレートを適用するか、アクセス、権限、および使用制限の細かくカスタマイズされた設定を選択できます。 たとえば、ユーザーは、組織内のユーザーのみがアクセスできるようにファイルを構成することも、ファイルの編集の可否、読み取り専用への制限、印刷防止などを制御することもできます。 時間が重要なファイルの場合、ファイルにアクセスできなくなる有効期限を (ユーザーが直接またはテンプレートの適用により) 構成できます。 Outlook の場合、ユーザーは、[**転送不可**] オプションを選択して、データの漏えいを防ぐこともできます。

### <a name="BKMK_ExchangeIntro"></a>Exchange Online と Exchange Server
Exchange Online または Exchange Server を使用する場合、追加の情報保護ソリューションを提供する Information Rights Management (IRM) 統合を使用できます。

-   **Exchange ActiveSync IRM**。モバイル デバイスで、保護された電子メール メッセージを保護および使用することができます。

-   **Outlook Web App** 用の RMS のサポート。これは、Outlook クライアントと同様に実装されるので、ユーザーは、テンプレートを使用するか個別のオプションを指定して電子メール メッセージを保護したり、自分に送信された保護された電子メール メッセージを読んで使用したりできます。

-   Outlook クライアントの**保護ルール**。管理者が構成し、RMS テンプレートを特定受信者向けの電子メール メッセージに自動的に適用されます。 たとえば、社内電子メールが法務部門に送信されるときに、法務部門の所属者のみが読むことが可能で、ただし転送できないようにすることができます。 送信前に電子メール メッセージに保護が適用されたことがユーザーに表示され、既定では、ユーザーは不要と判断した場合にそれを削除できます。 電子メールは送信される前に暗号化されます。 詳細については、Exchange ライブラリの「[Outlook 保護ルール](http://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)」と「[Outlook 保護ルールの作成](http://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)」を参照してください。

-   **トランスポート ルール**。管理者が構成し、送信者、受信者、メッセージの件名、および内容などのプロパティを基にして電子メール メッセージに RMS テンプレートを自動的に適用します。 これらは、概念的に保護ルールと似ていますが、ユーザーが保護を削除することはできず、Outlook Web Access とモバイル デバイスによって送信される電子メールに適用され、クライアントから送信される前に電子メール メッセージを暗号化しません。 詳細については、Exchange ライブラリの「[トランスポート保護ルールの作成](http://technet.microsoft.com/library/dd302432.aspx)」を参照してください。

-   **データ損失防止 (DLP) ポリシー**。このポリシーは、電子メール メッセージにフィルターを適用するための条件のセットを含み、機密コンテンツ (個人情報やクレジット カード情報など) のデータの損失を防ぐために役立つ操作を実行します。 ポリシーのヒントを使用すると、機密データが検出されたときに、電子メール メッセージ内の情報を基にして、情報保護の適用が必要な可能性があることをユーザーに警告することができます。 詳細については、Exchange ライブラリの「[データ損失防止](http://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)」を参照してください。

-   **Office 365 メッセージ暗号化**。トランスポート ルールを使用して暗号化された電子メールを社外のユーザーに送信し、Outlook Web App に似たブラウザーのインターフェイスで電子メールを読み取ります。 会社の暗号化された電子メールの免責事項のテキストとヘッダーのテキストをカスタマイズすることが可能で、会社のロゴを追加することもできます。 詳細については、Office Web サイトの「[Office 365 Message Encryption](http://office.microsoft.com/o365-message-encryption-FX104179182.aspx)」 を参照してください。

Exchange Server を使用する場合は、オンプレミス サーバーと RMS クラウド サービスの間のリレーとして機能する RMS コネクタをデプロイすることで、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] と情報保護機能を使用できます。 詳細については、「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」を参照してください。

### <a name="BKMK_SharePointIntro"></a>SharePoint Online と SharePoint Server
SharePoint Online または SharePoint Server を使用する場合に Information Rights Management (IRM) 統合を使用すると、管理者がリストやライブラリを保護し、ユーザーがドキュメントをチェックアウトしたときに、指定した情報保護ポリシーに従って許可されたユーザーのみがファイルを表示および使用できるようにファイルが保護されます。 たとえば、ファイルが読み取り専用のときに、テキストのコピーを無効にし、ローカル コピーの保存やファイルの印刷を防止することができます。

リストとライブラリについては、情報保護は常にエンド ユーザーではなく管理者によって適用されます。 また、個別のファイルではなくコンテナー内のすべてのドキュメントのリストまたはライブラリのレベルで適用されます。  SharePoint Online を使用する場合、ユーザーは OneDrive for Business ライブラリにも IRM を適用できます。

最初に SharePoint の IRM サービスを有効にする必要があります。 次に、ライブラリに対して Information Rights Management を指定します。 SharePoint Online と OneDrive for Business の場合、ユーザーは OneDrive for Business ライブラリに対しても Information Rights Management を指定できます。 SharePoint は権限ポリシー テンプレートを使用しませんが、SharePoint にはテンプレートで指定できる設定とほとんど同じでユーザーが選択できる構成設定があります。

SharePoint Server を使用する場合は、オンプレミス サーバーと RMS クラウド サービスの間のリレーとして機能する RMS コネクタをデプロイすることで、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] と情報保護機能を使用できます。 詳細については、「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」を参照してください。

> [!NOTE]
> 現在のところ、SharePoint で IRM を使用する場合、いくつかの制限があります。
> 
> -   Azure クラシック ポータルで管理する既定のテンプレートまたはカスタム テンプレートは使用できません。
> -   ファイル名拡張子が保護された PDF ファイルのための .PPDF であるファイルはサポートされていません。 ファイル名拡張子が .PDF で、RMS がネイティブで保護しているファイルは、RMS をネイティブでサポートする PDF リーダーを使用する場合にサポートされます。
> -   モバイル デバイスの Office では RMS がまだサポートされていないため、RMS で保護されているファイルを表示するにはこれらのデバイスでブラウザーを使用する必要があり、ファイルは読み取り専用です。

Azure RMS は、ドキュメントが SharePoint からダウンロードされる際には使用制限およびデータ暗号化を適用し、ドキュメントが最初に SharePoint で作成される場合、またはライブラリにアップロードされる際には適用しません。 ドキュメントをダウンロードする前に保護する方法については、SharePoint ドキュメントの「[OneDrive for Business および SharePoint Online のデータ暗号化](https://technet.microsoft.com/library/dn905447.aspx)」を参照してください。

SharePoint での Azure RMS の使用について詳しくは、Office のブログの次の投稿を参照してください: [SharePoint および SharePoint Online における Information Rights Management の新機能](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## <a name="BKMK_FCIIntro"></a>Windows Server を実行するファイル サーバーとファイル分類インフラストラクチャ (FCI) の使用
ファイル分類インフラストラクチャを使用するように Windows Server を構成すると、このファイル サーバー リソース マネージャーの機能でローカル ファイルをスキャンし、機密データが含まれているかどうかを判断することができます。 この条件を満たすファイルには、管理者が定義する分類プロパティのタグが付けられます。 その後で、ファイル分類インフラストラクチャが分類に従って自動操作を実行できます。 これらの操作には、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を使用した情報保護の適用や Rights Management コネクタ (RMS コネクタとも呼びます) の配置などがあります。 これにより Office ファイルは Azure RMS によって自動的に保護されます。

すべてのファイルの種類を保護する場合は、RMS コネクタを使用せずに、代わりに、[RMS 保護ツール](https://www.microsoft.com/en-us/download/details.aspx?id=47256)でコマンドレットを使用して Windows PowerShell スクリプトを実行できます。

この分類ポリシーは、完全に構成可能で拡張性が高いので、承認されていないユーザーおよび承認されたユーザーからの潜在的なデータの漏えいを防止できます。 管理者がファイルにアクセスする必要がないようなポリシーを構成できるので、ネットワーク管理者からのデータ漏えいのリスクも減らすことができます。

Office ファイル用 RMS コネクタをデプロイおよび構成する方法については、「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」を参照してください。

すべてのファイルの種類に Windows PowerShell スクリプトを使用する方法については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md)」を参照してください。

## <a name="BKMK_APIAppsIntro"></a>RMS API をサポートするその他のアプリケーション
RMS SDK を使用すると、社内開発者が、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] をネイティブでサポートする基幹業務アプリケーションを作成できます。 これらのアプリケーションと情報保護を統合する方法は、アプリケーションの作成方法によって決まります。 たとえば、ユーザーによる最小限の対話操作で統合を自動的に適用するか、またはより細かくカスタマイズされた場合は、ファイルの情報保護を適用するための設定を構成するようにユーザーに要求することができます。 SDK の詳細については、「[Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx)」を参照してください。

同様に、多くのソフトウェア ベンダーが情報保護ソリューションを提供するアプリケーションを提供しています。これらは ERM (Enterprise Rights Management) 製品とも呼ばれます。 一般的な例として、特定のプラットフォーム向けに [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] をサポートする PDF リーダーがあります。 「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」の「[クライアント デバイスの機能](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities)」セクションにある表を使用して RMS をサポートするアプリケーション (RMS 対応アプリケーション) を確認し、Web 検索を使用してアプリケーションを購入またはダウンロードすることができます。

> [!TIP]
> 新しくリリースされたアプリケーションの場合は、「[Azure Rights Management の情報とサポート](../Topic/Information_and_Support_for_Azure_Rights_Management.md)」に記載されている RMS コミュニティ チャネルを確認してください。

## 参照
[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)


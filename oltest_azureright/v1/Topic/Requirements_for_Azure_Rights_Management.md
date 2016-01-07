---
description: na
keywords: na
pagetitle: Requirements for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
---
# Azure Rights Management の要件
組織に Microsoft Azure Rights Management (Azure RMS) をデプロイするには、以下の要件を満たしていることを確認してください。 満たしていれば、[Azure Rights Management の展開ロードマップ](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) を使用して組織に Rights Management をデプロイできます。

|要件|詳細情報|
|------|--------|
|RMS のクラウド サブスクリプション|RMS をサポートするクラウド サブスクリプションが組織で必要です。<br /><br />ライセンスの情報については、このトピックの「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションを参照してください。|
|Azure AD ディレクトリ|RMS のユーザー認証をサポートするために組織で Azure AD ディレクトリが必要です。 また、内部設置型ディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。<br /><br />必要なクライアント ソフトウェアがあり、正しく構成されている場合、Azure RMS では多要素認証 (MFA) がサポートされます。MFA サポート インフラストラクチャ。<br /><br />詳細については、このトピックの「[Azure AD ディレクトリ](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_AzureADTenant)」セクションを参照してください。|
|クライアント デバイス|ユーザーは RMS をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を持っている必要があります。<br /><br />詳細については、このトピックの「[Azure RMS をサポートするクライアント デバイス](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices)」セクションを参照してください。|
|アプリケーション|ユーザーは、RMS をサポートするアプリケーションを実行する必要があります。<br /><br />詳細については、このトピックの「[Azure RMS をサポートするアプリケーション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications)」セクションを参照してください。|
|インターネットと依存クラウド サービスへの接続をサポートするインフラストラクチャ|特定の接続を許可するように構成する必要があるファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、「[Office 356 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」を参照してください。<br /><br />「**Office 356 ポータルと ID**」セクション内の URL および IP アドレスのリストは Office 365 ポータル、Azure Active Directory リソース、および Azure Rights Management に該当します。 RSS フィードを購読して最新の情報を入手するにはこの記事の手順を使用してください。<br /><br />Office の記事の情報に加えて、Azure RMS に固有の要件は以下のとおりです。<br /><br />-   TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、Azure RMS との通信を保護するのに RMS クライアントが Microsoft が管理する CA と使用する証明書のピン留めが解除されます。<br />-   ユーザーの代わりに認証を行う Web プロキシ構成を使用しないでください。|

オンプレミス サーバーで Azure RMS を使用する場合は、以下の製品がサポートされます。

-   Exchange Server

-   SharePoint Server

-   ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の Azure RMS 要件については、このトピックの「[Azure RMS をサポートするオンプレミス サーバー](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedServers)」を参照してください。

> [!IMPORTANT]
> 次のデプロイ シナリオはサポートされていません。
> 
> -   同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細は「[AD RMS から Azure Rights Management への移行](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md)」を参照)
> 
> 移行は、[AD RMS から Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) および [Azure RMS から AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx) の 2 つがサポートされています。 Azure RMS をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Rights Management の使用停止と非アクティブ化](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md)」を参照してください。

Azure RMS の要件の詳細について、以下のセクションで説明します。

## <a name="BKMK_SupportedSubscriptions"></a>Azure RMS をサポートするクラウド サブスクリプション
Azure RMS を使用するには、組織は次のサブスクリプションの少なくとも 1 つと、ユーザー、ファイル、および電子メール メッセージを保護するサービスの十分な数のライセンスを用意する必要があります。 ユーザー (ファイルや電子メール メッセージの所有者) に保護を適用できるサービスがある場合、そのようなユーザーにはこれらのライセンスの 1 つが必要になります。 この保護されたデータを利用するだけであれば (読み取りや編集など)、ライセンスは必要ありません。

-   Office 365

-   Azure Rights Management Premium (以前の Azure RMS Standalone)

-   エンタープライズ モビリティ スイート

-   個人用 RMS

詳細およびサインアップ オプションについては、以下のセクションを参照してください。

有料サブスクリプションの Azure RMS 機能のライセンスの比較については、「[Rights Management Services (RMS) の提供内容の比較](http://technet.microsoft.com/dn858608)」を参照してください。

### Office 365 サブスクリプション
[30 日間の無料試用版:Enterprise E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

このサブスクリプションは、Office Online Services と、その Information Rights Management 機能 (Azure RMS を使用) を使用する組織向けに設計されています。 ただし、Office 365 サブスクリプションには Azure RMS を含まないものもあります。

|ライセンス オプション|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 Education A1|Office 365 Enterprise E3<br /><br />Office 365 Education A3<br /><br />Office 365 Government G3|Office 365 Enterprise E4<br /><br />Office 365 Education A4<br /><br />Office 365 Government G4|Office 365 Enterprise E5<br /><br />Office 365 Education A5<br /><br />Office 365 Government G5|Office 365 Enterprise K1|SharePoint Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|---------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Information Rights Protection (IRM)|いいえ|いいえ|いいえ|はい|はい|はい|いいえ|いいえ|いいえ|

### Azure Rights Management Premium サブスクリプション
[30 日間の無料試用版](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

このサブスクリプションは以前 Azure RMS Standalone という名前で知られており、Azure RMS を使用したいが Azure RMS を含むサブスクリプションを持っていない組織を対象としています。 たとえば Office 365 Business Essentials または Office 365 Enterprise E1 のサブスクリプションを持っている場合、これらのサブスクリプションには Azure RMS が含まれません (前のセクションの表を参照してください)。 Azure RMS を使用するには、Azure Rights Management Premium のサブスクリプションを購入してください (または Office 365 Enterprise E4 など、Azure RMS をサポートする別のサブスクリプションを購入してください)。

詳細については、「[Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management)」を参照してください。

また、このサブスクリプションには、25 ユーザーを対象に Azure RMS を試用するための無料試用期間が含まれています。 代替用のサブスクリプションを購入する前に評価版サブスクリプションが期限切れになった場合は、次の「評価版サブスクリプションの期限が切れた場合」セクションを参照してください。

|ライセンス オプション|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 Education A1|Office 365 Enterprise E3<br /><br />Office 365 Education A3<br /><br />Office 365 Government G3|Office 365 Enterprise E4<br /><br />Office 365 Education A4<br /><br />Office 365 Government G4|Office 365 Enterprise E5<br /><br />Office 365 Education A5<br /><br />Office 365 Government G5|Office 365 Enterprise K1|SharePoint Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|---------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Information Rights Protection (IRM)|はい|はい <sup>1</sup>|はい|はい|はい|はい|はい|はい|はい|
<sup>1</sup> Business Premium の場合はクライアントの制限があります。Outlook Web App および RMS 共有アプリを使用することにより、RMS でコンテンツを保護し、保護されたコンテンツを使用できます。 Office Online および Office 365 Business Premium 用のクライアント アプリケーションなど、他のすべての Office アプリケーションを使用して、保護されたコンテンツを利用できます。

#### <a name="BKMK_TrialExpiryBehavior"></a>評価版サブスクリプションの期限が切れた場合
評価版サブスクリプションの期限が切れた場合は、Azure RMS の評価版サブスクリプションによって保護されていたコンテンツへのアクセスが失われます。 ただし、Azure RMS をサポートするサブスクリプションを購入すれば、アクセスは自動的に回復します。

例外として、評価版サブスクリプションを取得する前に組織が個人用 RMS サブスクリプションを通して Azure RMS を使用していた場合に限り、期限切れでアクセスが失われることはありません。 この場合、評価版サブスクリプションの期限が切れた後も保護されていたコンテンツへのアクセスは保持されます。

### エンタープライズ モビリティ スイート サブスクリプション
[30 日間の無料試用版](http://go.microsoft.com/fwlink/?LinkId=615385)

このサブスクリプションは、Azure Active Directory Premium、Windows Intune、および Azure Rights Management を組み合わせて使用する組織向けに設計されています。 詳細については、[マイクロソフト エンタープライズ モビリティの概要](http://go.microsoft.com/fwlink/?LinkId=615386)に関するページを参照してください。

|ライセンス オプション|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 Education A1|Office 365 Enterprise E3<br /><br />Office 365 Education A3<br /><br />Office 365 Government G3|Office 365 Enterprise E4<br /><br />Office 365 Education A4<br /><br />Office 365 Government G4|Office 365 Enterprise E5<br /><br />Office 365 Education A5<br /><br />Office 365 Government G5|Office 365 Enterprise K1|SharePoint Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|---------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Information Rights Protection (IRM)|はい|はい <sup>1</sup>|はい|はい|はい|はい|はい|はい|はい|
<sup>1</sup> Business Premium の場合はクライアントの制限があります。Outlook Web App および RMS 共有アプリを使用することにより、RMS でコンテンツを保護し、保護されたコンテンツを使用できます。 Office Online および Office 365 Business Premium 用のクライアント アプリケーションなど、他のすべての Office アプリケーションを使用して、保護されたコンテンツを利用できます。

### 個人用 RMS サブスクリプション
このサブスクリプションは、Azure RMS または AD RMS を展開していない組織の個人ユーザー向けに設計されています。 このようなユーザーが Azure RMS を使用して、組織によって保護されているコンテンツを読んだり、各自のコンテンツを保護したりできます。

詳細については、「[個人用 RMS と Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)」を参照してください。

## <a name="BKMK_AzureADTenant"></a>Azure AD ディレクトリ
Azure RMS を使用するには、Azure AD ディレクトリが必要です。 このディレクトリの組織アカウントを使用して Azure クラシック ポータルにサインインします。ここでは、たとえば、Rights Management テンプレートを構成および管理することができます。

組織の Azure サブスクリプションがまだない場合は、無料評価版にサインアップして取得できます。「[はじめに - Windows Azure](https://account.windowsazure.com/organization)」ページにアクセスし、指示に従ってください。

詳細については、Azure Active Directory ドキュメントの次のリソースを参照してください。

-   [Azure AD ディレクトリとは](http://msdn.microsoft.com/en-us/library/185da266-58a9-43e6-9c66-2c8f702545c6)

-   [Azure サブスクリプションを Azure AD に関連付ける方法](http://msdn.microsoft.com/en-us/library/edf05c2e-944a-4da5-a330-dc9dc479f127)

Azure AD ディレクトリをオンプレミス AD フォレストと統合する場合は、[ディレクトリ統合](http://msdn.microsoft.com/en-us/library/bf82bdff-2467-403b-8c1a-0e9eebcf31e8)に関するページを参照してください。

> [!NOTE]
> AD FS または同等な認証プロバイダーを使用してオンプレミスで認証を行うモバイル デバイスまたは Mac コンピューターの場合:
> 
> -   最小サーバー バージョンの **Windows Server 2012 R2** で AD FS を使用するか、または OAuth 2.0 プロトコルをサポートするその他の認証プロバイダーを使用する必要があります。

### <a name="BKMK_MFA"></a>多要素認証 (MFA) と Azure RMS
Azure RMS で多要素認証 (MFA) を使用するには、次のうち 1 つ以上が必要です。

-   Office 2013 (最小バージョン):

    -   Office 2013 をお持ちの場合、[2015 年 6 月 9 日付 Office 2013 用更新プログラム (KB3054853)](https://support.microsoft.com/kb/3054853) を必ずインストールしてください。 この更新プログラムの詳細や、Active Directory 認証ライブラリ (ADAL) を用いた最新の認証による Office 2013 へのサインインの詳細については、「[Office 2013 最新認証パブリック プレビューの公開](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)」 (Office ブログの投稿) をご覧ください。

-   Windows 用 Rights Management 共有アプリケーション:

    -   最小バージョン 1.0.1908.0 がインストールされている必要があります。バージョンはコントロール パネルの [プログラムと機能] で確認できます。 共有アプリケーションの詳細については、「[Windows 用 Rights Management 共有アプリケーション](../Topic/Rights_Management_Sharing_Application_for_Windows.md)」をご覧ください。

-   モバイル デバイス用や Mac コンピューター用の Rights Management 共有アプリ:

    -   最新バージョンがインストールされていることをご確認ください。 MFA では、2015 の年 9 月以降にリリースされた RMS 共有アプリがサポートされます。

確認後、MFA ソリューションを構成します。

-   Microsoft が管理するテナント (Azure Active Directory または Office 365) の場合:

    -   Azure MFA を構成してユーザー向けに MFA を適用します。 手順については、Azure ドキュメントの「[クラウドでの Azure Multi-Factor Authentication Server の概要](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/)」をご覧ください。

        Azure MFA の詳細については、「[Azure Multi-Factor Authentication とは](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)」をご覧ください。

-   統合テナント (オンプレミスのフェデレーション サーバー) の場合:

    -   ご利用のフェデレーション サーバーを Azure Active Directory または Office 365 向けに構成します。たとえば AD FS をご使用の場合は、TechNet の記事「[AD FS の追加の認証方法の構成](https://technet.microsoft.com/library/dn758113.aspx)」をご覧ください。

        このシナリオの詳細については、Office ブログの記事「[Office 365 の機能 – 合理化された ID プログラム」](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) (Office ブログの投稿) をご覧ください。

## <a name="BKMK_SupportedDevices"></a>Azure RMS をサポートするクライアント デバイス
次のセクションでは、Azure Rights Management (RMS) をサポートするデバイスと、それらがサポートする RMS 機能について説明します。

-   [コンピューター](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedComputers)

-   [モバイル デバイス](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedMobileDevices)

-   [クライアント デバイスの機能](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities)

### <a name="BKMK_RMSSupportedComputers"></a>コンピューター
次のコンピューター オペレーティング システムで Azure Rights Management がサポートされています。

-   **Windows 7** (x86、x64)

-   **Windows 8** (x86、x64)

-   **Windows 8.1** (x86、x64)

-   **Windows 10** (x86、x64)

-   **Mac OS X**:Mac OS X 10.8 (Mountain Lion) 以降

### <a name="BKMK_RMSSupportedMobileDevices"></a>モバイル デバイス
次のモバイル デバイス オペレーティング システムで Azure Rights Management がサポートされています。

-   **Windows Phone**:Windows Phone 8.1

-   **Android 端末およびタブレット**:Android 4.0.3 以降

-   **iPhone および iPad**:iOS 7.0 以降

-   **Windows RT タブレット**:Windows 8 RT、Windows 8.1 RT

### <a name="BKMK_ClientCapabilities"></a>クライアント デバイスの機能
現在のところ、サポートされるクライアント デバイスの一部では一部の RMS 機能がサポートされていません。 次の表を利用し、RMS 機能をサポートするアプリケーションと例外を特定してください。

別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 また、iOS、Android、OS X、Windows Phone 8.1 で AD RMS をサポートするには、[Active Directory Rights Management Services モバイル デバイス拡張機能](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341)が必要です。

表の列に関する情報

-   **保護された PDF**:このファイルの拡張子は .ppdf です。RMS 共有アプリケーションを使用して Office ファイルや PDF ファイルを電子メールで共有すると、自動的に作成されます。 RMS 共有アプリケーションには、保護された PDF ファイル用のリーダーが含まれています。 以前に Azure RMS または AD RMS を使用して保護された PDF ファイルを作成していた場合は、Windows、iOS、および Android デバイス上で Foxit Reader および Nitro Pro を使用して、引き続きこれらのファイルを読み取ることができます。

-   **電子メール:**表示されている電子メール クライアントは、電子メール メッセージを保護できるので、添付されているファイルも自動的に保護されます。 このシナリオでは、クライアントのプレビュー機能で、許可された受信者に対して保護されたコンテンツ (メッセージと添付ファイル) を表示できます。 ただし、電子メール メッセージが保護さておらず、添付ファイルが保護されている場合、クライアントのプレビュー機能では、許可された受信者に対する場合も保護された添付ファイルを表示できません。

-   **他のファイルの種類**:テキスト ファイルと画像ファイルには、.txt、.xml、.jpg、.jpeg などのファイル名拡張子が付いているファイルがあります。 これらのファイルでは、RMS によりネイティブで保護された後に、ファイル名拡張子が変更され、読み取り専用になります。 ネイティブで保護できないファイルでは、RMS によって一般的に保護された後に、ファイル名拡張子が .pfile になります。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)」の「[保護のレベル – ネイティブと汎用](https://technet.microsoft.com/library/dn339003.aspx)」および**externalLink tag is not supported!!!!**
    」セクションを参照してください。

|**デバイス オペレーティング システム**|Word、Excel、PowerPoint|保護された PDF|Email|他のファイルの種類|
|--------------------------|-------------------------|-------------|---------|-------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office モバイル アプリ (Azure RMS のみ) <sup>1</sup><br /><br />Office Online<sup>2</sup>|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共有アプリ|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA)<sup>3</sup><br /><br />Windows メール<sup>4</sup>|Windows 用 RMS 共有アプリケーションテキスト、画像、pfile<br /><br />Siemens JT2Go:JT ファイル (Windows 10 のみ)|
|**iOS**|Office for iPad および Office for iPhone<sup>5</sup><br /><br />Office Online<sup>2</sup><br /><br />TITUS Docs|Foxit Reader<br /><br />RMS 共有アプリ<sup>1</sup><br /><br />TITUS Docs|NitroDesk<sup>4</sup><br /><br />iPad および iPhone 用 Outlook<sup>4</sup><br /><br />OWA for iOS<sup>3</sup><br /><br />Secure Islands IQProtector<sup>1</sup><br /><br />TITUS Mail|RMS 共有アプリ<sup>1</sup>:テキスト、画像、pfile<br /><br />TITUS Docs:Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online<sup>2</sup>|GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS 共有アプリ<sup>1</sup>|9Folders<sup>4</sup><br /><br />GigaTrust App for Android<sup>4</sup><br /><br />NitroDesk<sup>4</sup><br /><br />OWA for Android<sup>3</sup> <sup>6</sup><br /><br />Samsung Email (S3 以降)<sup>6</sup><br /><br />Secure Islands IQProtector<sup>1</sup><br /><br />TITUS Classification for Mobile|RMS 共有アプリ<sup>1</sup>:テキスト、画像、pfile|
|**OS X**|Office 2011 (AD RMS のみ)<br /><br />Office 2016 for Mac<br /><br />Office Online<sup>2</sup>|Foxit Reader<br /><br />RMS 共有アプリ<sup>1</sup>|Outlook 2011 (AD RMS のみ)<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共有アプリ<sup>1</sup>:テキスト、画像、pfile|
|**Windows RT**|Office 2013 RT<br /><br />Office Online<sup>2</sup>|サポートされていません|Outlook 2013 RT<br /><br />Windows 用のメール アプリ<br /><br />Windows メール<sup>4</sup>|Siemens JT2Go:JT ファイル|
|**Windows Phone 8.1**|Office Mobile (AD RMS のみ)|RMS 共有アプリ<sup>1</sup>|Outlook Mobile<sup>4</sup>|RMS 共有アプリ<sup>1</sup>:テキスト、画像、pfile|
|**Blackberry 10**|サポートされていません|サポートされていません|Blackberry の電子メール<sup>4</sup>|サポートされていません|
<sup>1</sup> 保護されたコンテンツの表示をサポートします。

<sup>2</sup> SharePoint Online、OneDrive for Business、Outlook Web Access での保護されたコンテンツの表示をサポートします。

<sup>3</sup> 受信者が Exchange On-premises にメールボックスを所有していて、保護された電子メールを受信した場合、このコンテンツは、Outlook などの機能の豊富な電子メール クライアントでのみ開くことができます。  このコンテンツは Outlook Web Access から開くことはできません。

<sup>4</sup> Exchange ActiveSync IRM を使用します。Exchange の管理者が有効にする必要があります。 ユーザーは保護された電子メール メッセージを表示、返信、全員に返信することができますが、新しい電子メール メッセージを自身で保護することはできません。

受信者が Exchange On-premises にメールボックスを所有していて、Exchange を使用している別の組織から保護された電子メールを受信した場合、このコンテンツは、Outlook などの機能豊富な電子メール クライアントでのみ開くことができます。  このコンテンツは、Exchange Active Sync IRM を使用するデバイスから開くことはできません。

<sup>5</sup> 保護されたドキュメントの表示と編集をサポートします。 詳細については、Office ブログの次の投稿を参照してください。[iPad および iPhone 用 Office で Azure Rights Management のサポートを開始](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

<sup>6</sup> 詳細については、Office ブログの次の投稿をご覧ください。[OWA for Android は選択したデバイスで利用可能](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

> [!TIP]
> さまざまなプラットフォーム向けの Office での今後の RMS サポートの詳細については、Office のブログの次の投稿を参照してください。[あらゆる場所で Office、あらゆる場所で暗号化](http://blogs.office.com/2015/02/18/office-everywhere-encryption-everywhere/)

## <a name="BKMK_SupportedApplications"></a>Azure RMS をサポートするアプリケーション
次のアプリケーションで Azure RMS がネイティブにサポートされています。RMS API を使用することで RMS はこれらのアプリケーションと緊密に統合され、使用制限がサポートされます。 このようなアプリケーションは RMS 対応とも呼ばれます。

-   次のスイートに含まれる **Microsoft Office アプリケーション** (Word、Excel、PowerPoint、Outlook) は、Azure RMS を使用してコンテンツを保護できます。

    -   Office 365 ProPlus

    -   Office 365 Enterprise E3

    -   Office 365 Enterprise E4

    -   Office 365 Enterprise E5

    -   Office Professional Plus 2016

    -   Office Professional Plus 2013

    -   Office Professional Plus 2010

    Office の他のエディション (Office 2007 を除く) は、保護されたコンテンツを使用できます。

    > [!NOTE]
    > Azure RMS と Office Professional Plus 2010 または Office Professional 2010:
    > 
    > -   Windows 用 Rights Management 共有アプリケーションが必要です
    > -   Windows 10 ではサポートされていません

-   **Windows 用 Rights Management 共有アプリケーション**

    Windows 用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

    -   [Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003.aspx)

    -   [Rights Management 共有アプリケーション ユーザー ガイド](http://technet.microsoft.com/library/dn339006.aspx)

-   **モバイル プラットフォーム用 Rights Management 共有アプリケーション**

    モバイル プラットフォーム用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

    -   [Microsoft Rights Management のページ](http://go.microsoft.com/fwlink/?LinkId=303970)にあるリンクを使用して関連アプリをダウンロードする

    -   Microsoft Intune を使用してモバイル デバイスを管理する場合は、アプリを[ポリシー管理型アプリとして iOS および Android デバイス](https://technet.microsoft.com/library/dn878026.aspx)にデプロイして構成できます。

    -   [モバイル プラットフォーム用 Microsoft Rights Management 共有アプリケーションの FAQ](http://technet.microsoft.com/dn451248)

-   **RMS API をサポートする他のアプリケーション**:

    -   RMS SDK を使用して社内で作成した基幹業務アプリケーション

    -   RMS SDK を使用してソフトウェア ベンダーが作成したアプリケーション

    SDK の詳細については、「[Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx)」を参照してください。

> [!IMPORTANT]
> Azure RMS では、現在のところ以下のアプリケーションはサポートされません。
> 
> -   Microsoft Office for Mac 2011
> -   Microsoft OneDrive for Business for SharePoint Server 2013
> -   XPS ビューアー
> 
> また、RMS 共有アプリケーションには次の制限事項があります。
> 
> -   Windows コンピューター:Windows 7 Service Pack 1 以降が必要です

これらのアプリケーションによる Azure RMS のサポート状況の詳細については、「[アプリケーションで Azure Rights Management をサポートする方法](../Topic/How_Applications_Support_Azure_Rights_Management.md)」を参照してください。

構成方法については、「[Azure Rights Management 用にアプリケーションを構成する](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)」を参照してください。

## <a name="BKMK_SupportedServers"></a>Azure RMS をサポートするオンプレミス サーバー
Azure RMS コネクタを使用する場合、次のオンプレミス サーバー製品で Azure RMS がサポートされます。このコネクタがオンプレミス サーバーと Azure RMS との通信インターフェイス (リレー) として動作します。 さらに、この構成では Active Directory フォレストと Azure Active Directory とのディレクトリ同期を構成する必要があります。

-   **Exchange Server**:

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Windows Server 2008 R2 を実行するファイル サーバーには、RMS の保護を適用する組み込みのファイル管理タスク アクションがないため、このシナリオには RMS コネクタを使用できません。 ただし、Azure RMS を使用してファイルを保護できる実行可能ファイルまたはスクリプトを実行するカスタムのファイル管理タスクを構成する場合、これらのオペレーティング システムでファイル分類インフラストラクチャと Azure RMS を使用できます。 たとえば、[RMS Protection コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)を使用する Windows PowerShell スクリプトなどがあります。
    > 
    > 最新の Windows Server を実行しているサーバーでこれらのコマンドレットを使うこともできます。この場合、すべてのファイル タイプが保護されるという利点があります。 RMS コネクタでは Office ファイルのみ保護されます。 方法については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md)」を参照してください。

RMS コネクタは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 でサポートされています。

これらのオンプレミス サーバーで RMS コネクタを構成する方法の詳細については、「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」を参照してください。

## 参照
[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)


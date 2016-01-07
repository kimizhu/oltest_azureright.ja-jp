---
description: na
keywords: na
pagetitle: Frequently Asked Questions for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
---
# Azure Rights Management に関してよく寄せられる質問
Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) に関してよく寄せられる質問をいくつか紹介します。

## Azure RMS の展開の要件と、展開を開始する方法について教えてください。
最初に「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」を確認してください。使用可能なクラウド サブスクリプション、オンプレミス サーバーで Azure RMS を使用する方法、現時点でサポートされていないデプロイメント シナリオ、Azure RMS をサポートするデバイスとアプリケーションについての情報と、ファイアウォールまたはプロキシ サーバーの IP アドレスとドメイン名の一覧へのリンクが記載されています。 また、「[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)」セクションに含まれる他のトピックを確認すると、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] による組織のデータ保護とアプリケーション連携のしくみや、オンプレミス バージョンの Active Directory Rights Management との比較結果について基本的な知識を得ることができ、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] に固有の用語と略語について理解することができます。

Azure RMS のテストまたは組織へのデプロイを行う準備ができたら、「[Azure Rights Management の展開ロードマップ](../Topic/Azure_Rights_Management_Deployment_Roadmap.md)」で、デプロイの手順の一覧と、各手順の詳細や具体的な操作手順へのリンクを参照できます。

その他の情報、リソース、およびサポート オプションが必要な場合は、「[Azure Rights Management の情報とサポート](../Topic/Information_and_Support_for_Azure_Rights_Management.md)」を参照してください。

## Azure RMS はオンプレミス サーバーと統合できますか。
はい。 Azure RMS は、Exchange Server、SharePoint、Windows ファイル サーバーなどのオンプレミス サーバーと統合できます。 統合するには、[Rights Management コネクタ](https://technet.microsoft.com/library/dn375964.aspx)を使用します。 または、Windows Server でファイル分類インフラストラクチャ (FC) を使用することのみを目的とされている場合は、[RMS 保護コマンドレット](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx)を使用できます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure RMS で XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure RMS での証明書の使用方法については、「[Azure Active Directory Rights Management の概要](../Topic/What_is_Azure_Rights_Management_.md)」トピックの[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Walthrough)セクションをご覧ください。

## 一部のユーザーが Exchange Online 上の Exchange に、他のユーザーが Exchange Server 上の Exchange に登録されているハイブリッド デプロイメント構成です。この構成は、Azure RMS でサポートされていますか。
はい、サポートされています。また、2 つの Exchange デプロイメント間でシームレスに電子メールと添付ファイルを保護し、保護された電子メールと添付ファイルを使用できるようになることがメリットです。 この構成の場合、[Azure RMS をアクティブ化し](https://technet.microsoft.com/library/jj658941.aspx)、[IRM for Exchange Online を有効にして](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)、[RMS コネクタをデプロイして](https://technet.microsoft.com/library/dn375964.aspx) Exchange Server 用に構成します。

## 運用環境に Azure RMS をデプロイすると、会社の環境が Azure RMS に固定されたり、Azure RMS で保護したコンテンツにアクセスできなくなる危険性が生じたりしますか。
いいえ。データを常に制御することができます。また、たとえ Azure RMS の使用を停止したとしても、継続してデータにアクセスすることができます。 詳細については、「[Azure Rights Management の使用停止と非アクティブ化](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md)」を参照してください。

ただし、Azure RMS のデプロイメントを停止される前に、お客様が使用を停止する理由を伺う機会をいただいています。 Azure RMS がビジネス要件を満たしていない場合は、近い将来に新機能が計画されているか、代替案がないかをお問い合わせください。 お問い合わせの電子メールは [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) に送信してください。技術とビジネスの要件について説明いたします。

## Azure RMS を使用してコンテンツを保護するユーザーを制御できますか。
はい。Azure RMS には、このシナリオ用のユーザーのオンボーディング コントロールがあります。 詳細については、「[Rights Management をアクティブにする](../Topic/Activating_Azure_Rights_Management.md)」トピックの「[段階的デプロイのオンボーディング コントロールの構成](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls)」セクションを参照してください。

## ユーザーが、保護されたドキュメントを特定の組織と共有しないようにすることはできますか。
Azure RMS の最大の利点の 1 つは、Azure AD が認証を自動的に処理するため、各パートナー組織に対して明示的な信頼を構成することなく、企業間のコレボレーションをサポートできることです。

ユーザーが特定の組織とのドキュメントの安全な共有を防止するような管理オプションはありません。 たとえば、信頼していない組織や、競合先の組織をブロックするとします。 Azure RMS がこれらの組織のユーザーに保護されたドキュメントを送信しないようにしても意味がありません。その場合、ユーザーはドキュメントを保護されていないまま共有することになり、おそらくこれはこのシナリオにおいて最も望ましくない状況です。 たとえば、これらの組織のユーザーと社外秘ドキュメントを共有しているユーザーを識別することはできませんが、ドキュメント (または電子メール) が Azure RMS で保護されていれば、これが可能になります。

## 保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。
Azure RMS は、常にユーザー認証に Azure Active Directory アカウントと関連付けられた電子メール アドレスを使用します。これは、管理者にとって企業間のコラボレーションをシームレスにします。 他の組織で Azure サービスを使用する場合は、アカウントがオンプレミスで作成、管理されてから Azure に同期される場合でも、ユーザーは既に Azure Active Directory にアカウントを持っています。  組織が内部的に Office 365 を所有している場合、このサービスはユーザー アカウント用に Azure Active Directory も使用します。  ユーザーの組織が Azure に管理アカウントを持っていない場合、ユーザーは[個人用 RMS](https://technet.microsoft.com/library/dn592127.aspx) にサインアップできます。これは、管理されていない Azure テナントと組織用のディレクトリをユーザー用のアカウントを使用して作成するため、このユーザーは Azure RMS に対して認証されます。

このようなアカウントの認証方法は、他の組織の管理者が Azure Active Directory アカウントを構成している方法によって異なります。 たとえば、これらのアカウント用に作成されたパスワード、多要素認証 (MFA)、フェデレーション、Active Directory ドメイン サービスで作成されたパスワードを使用してから、Azure Active Directory に同期される場合があります。

## 社外のユーザーをカスタム テンプレートに追加できますか。
はい。  エンドユーザー (と管理者) がアプリケーションから選択できるカスタム テンプレートを作成すると、指定した定義済みのポリシーを使用して、すばやく簡単に情報保護を適用できます。 テンプレートの設定の 1 つに、コンテンツにアクセス可能なユーザーの設定があります。組織内のグループとユーザー、および組織外のユーザーを指定できます。

組織外のユーザーを指定するには、[Azure Rights Management 用 Windows PowerShell モジュール](https://technet.microsoft.com/library/jj585012.aspx)を使用します。

-   **権限定義オブジェクトを使用してテンプレートを作成または更新する**。    権限定義オブジェクトで外部電子メール アドレスおよびその権限を指定し、これを使用してテンプレートを作成または更新します。[New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) コマンドレットを使用して権限定義オブジェクト指定し、変数を作成してから、[Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) コマンドレット (新しいテンプレート用) または [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) コマンドレット (既存のテンプレートを変更する場合) を使用して、この変数を -RightsDefinition パラメーターに指定します。 ただし、これらのユーザーを既存のテンプレートに追加する場合は、外部ユーザーだけでなく、テンプレートに既存のグループの権限定義オブジェクトを定義する必要があります。

カスタム テンプレートの詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md)」を参照してください。

## Azure RMS でサポートされているデバイスとファイルの種類を教えてください。
サポートされるデバイスの一覧については、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」トピックの「[Azure RMS をサポートするクライアント デバイス](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices)」セクションを参照してください。 サポートされるデバイスによっては一部の RMS 機能がサポートされていないため、同じトピックにある「[クライアント デバイスの機能](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities)」の表も確認してください。

Azure RMS はすべてのファイルの種類をサポートできます。 テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、他のいくつかのアプリケーションのファイルの種類については、Azure RMS は暗号化と権限の適用 (アクセス許可) の両方を含むネイティブな保護を提供します。 他のすべてのアプリケーションとファイルの種類については、ファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証という一般的な保護機能が提供されます。

Azure RMS でネイティブでサポートされるファイル名拡張子の一覧については、「[Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003.aspx)」の「[サポートされているファイルの種類とファイル名拡張子](http://technet.microsoft.com/library/dn339003.aspx)」セクションを参照してください。 一覧に含まれないファイル名拡張子は、一般保護をこれらのファイルに自動的に適用する RMS 共有アプリケーションを使用することによってサポートされます。

## AD RMS からの移行はいつサポートされますか。
当初、Azure RMS は AD RMS などの Rights Management のオンプレミス デプロイからの移行をサポートしていませんでした。 ただし、現在ではサポートしています。

詳細については、「[AD RMS から Azure Rights Management への移行](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md)」を参照してください。

## BYOK と Azure RMS を併用したいのですが、BYOK は Exchange Online と互換性がないと知りました。何かアドバイスはありますか。
現在のこの制限で、Azure RMS のデプロイメントを延期しないでください。 Exchange Online をお持ちで、Bring Your Own Key (BYOK) を使用する場合は、当面 Azure RMS を既定のキー管理モード (キーの生成と管理を Microsoft で行う) でデプロイすることをお勧めします。 この方法を採用すると、重要なファイルと電子メールを保護する機能をすぐに活用し、後で (たとえば Exchange Online が BYOK をサポートするようになったときなどに) BYOK に移行することができます。

ただし、会社のポリシーでハードウェア セキュリティ モジュール (HSM) を使用する必要があり、そのために Azure RMS をデプロイできない場合は、Azure RMS をデプロイし、Exchange の RMS 機能を減らして BYOK を併用する方法があります。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」トピックの「[BYOK の料金と制限事項](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing)」セクションを参照してください。

## 必要な機能があるのですが、SharePoint で保護されたライブラリには使用できないようです。この機能のサポートは予定されていますか。
現在のところ、SharePoint は、IRM で保護されたライブラリを使用して、RMS で保護されたドキュメントをサポートしています。IRM で保護されたライブラリは、カスタム テンプレート、ドキュメントの追跡などの機能をサポートしていません。  詳細については、「[アプリケーションで Azure Rights Management をサポートする方法](../Topic/How_Applications_Support_Azure_Rights_Management.md)」トピックの[SharePoint Online と OneDrive for Business:IRM 構成](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline)セクションをご覧ください。

まだサポートされていない機能に関心がある場合は、[RMS チーム ブログ](http://blogs.technet.com/b/rms/)のお知らせに注意してください。

## ユーザーが社内や社外の人間とファイルを安全に共有できるように SharePoint Online で OneDrive for Business を構成するには、どうすればよいですか。
既定では、Office 365 管理者は構成しません。ユーザーが構成します。

SharePoint サイト管理者が、所有する SharePoint ライブラリの IRM を有効にして構成するのと同じように、OneDrive for Business は、ユーザーが自身の OneDrive for Business ライブラリの IRM を有効にして構成するように設計されています。  ただし、PowerShell を使用して、ユーザーに代わってこの処理を行うことができます。 手順については、「[Azure Rights Management 用にアプリケーションを構成する](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)」の記事の「[SharePoint Online と OneDrive for Business:IRM 構成](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline)」セクションを参照してください。

## RMS を正常に展開するためのヒントやコツがあれば教えてください。
これまでに多数の展開をサポートし、顧客、パートナー、コンサルタント、サポート エンジニアから話を聞いてきた経験から言える一番のヒントは、**シンプルな権限ポリシーを設計してデプロイすること**です。

Azure RMS では、他のユーザーと情報を安全に共有できるため、情報保護の範囲を詳細に指定することができます。 しかし、権限ポリシーはできるだけシンプルにしてください。 多くの組織にとって、Azure RMS の導入による業務上最も重要な利点は、既定の権限ポリシー テンプレートを適用して組織内のユーザーのアクセス許可を制限し、データ漏えいを防止できることです。 もちろん、印刷や編集などの操作を制限する必要があれば、より詳細なポリシーを作成することもできます。ただし、そのような細かい制限は、高レベルのセキュリティが必要なドキュメントに限定してください。最初から制限の厳しいポリシーを作成するのではなく、段階的に計画して作成していくことをお勧めします。

## Azure RMS の各サブスクリプションで使用できる機能と使用できない機能を教えてください。
Azure RMS (Office 365、Azure RMS Premium、および Enterprise Mobility Suite) をサポートする有料サブスクリプションの場合、サポートされる RMS 機能の一部に違いがあります。 機能の一覧については、「[Rights Management サービス (RMS) オファリングの比較](http://technet.microsoft.com/dn858608)」を参照してください。

Azure RMS (個人用の RMS) をサポートする無料サブスクリプションは、Azure RMS で保護されているコンテンツの使用をサポートしています。 詳細については、「[個人用 RMS と Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)」を参照してください。

## 無料の Azure RMS サブスクリプション (個人用 RMS) に関する技術情報 (たとえば、そのしくみ、アカウントを制御する方法、使用できないドメイン) はどこで入手できますか。
これらの質問に対する回答については、「[個人用 RMS と Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)」トピックを参照してください。

## 退職した従業員が保護していたファイルにアクセスするには、どうすればよいですか。
Azure RMS のスーパー ユーザー機能を使用してください。スーパー ユーザー権限を持つユーザーは、組織の RMS テナントから付与されたすべての使用ライセンスについて、完全な所有者権限を持ちます。 また必要に応じて、スーパー ユーザー機能を使用すると、権限を持つサービスのインデックス化とファイルの検証を行うことができます。

詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md)」を参照してください。

## Rights Management は画面キャプチャを防止できますか。
Rights Management は、一般的に使用されるほとんどの画面キャプチャ ツールからの画面キャプチャをブロックします。これにより、重要な情報や機密情報の偶発的または過失による漏えいの防止に役立ちます。 ただし、画面に表示されるデータをユーザーが共有するにはさまざまな方法があり、スクリーン ショットを保存する方法はその 1 つにすぎません。 たとえば、表示される情報を共有しようとするユーザーは、カメラ付き携帯電話を使用して写真を撮影したり、データを再入力したり、単に口頭で他者に伝達することができます。

これらの例が示すように、共有してはならないデータをユーザーが共有することを、技術だけで必ずしも防止できるわけではありません。 Rights Management は、承認および使用ポリシーを使用して重要なデータを保護するのに役立つものの、このエンタープライズ権限管理ソリューションは、他のコントロールと共に使用する必要があります。 たとえば、物理的なセキュリティを実装したり、組織のデータへのアクセスが承認されているユーザーを慎重に検査および監視したり、共有してはならないデータを理解できるようにユーザーの教育に投資したりすることです。

## 法律、法令遵守、SLA など、Azure RMS に関するサポート情報はどこで入手できますか。
Azure RMS は他のサービスをサポートし、また、他のサービスに依存しています。 Azure RMS サービスの使用方法以外で、Azure RMS の関連情報をお探しの場合は、以下のリソースを参照してください。

**法律およびプライバシー:**

-   Microsoft Azure の契約情報について:[Microsoft Azure の契約](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Microsoft Azure のプライバシー情報について:[Microsoft Azure のプライバシーに関する声明](http://azure.microsoft.com/support/legal/privacy-statement/)

**セキュリティ、コンプライアンス、監査:**

「[Azure Active Directory Rights Management の概要](../Topic/What_is_Azure_Rights_Management_.md)」トピックの[セキュリティ、コンプライアンス、および規制の要件](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMScompliance)セクションをご覧ください。 さらに

-   Azure RMS の外部認証について:[Microsoft Azure トラスト センター](http://azure.microsoft.com/support/trust-center/)

-   FIPS 140 について:[FIPS 140 検証](https://technet.microsoft.com/library/security/cc750357.aspx)

**サービス レベル アグリーメント:**

-   主な国ごとの Azure RMS のサービス レベル アグリーメント:[サービス レベル アグリーメント](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

-   Azure Active Directory のサービス レベル アグリーメント:[サービス レベル アグリーメント](http://azure.microsoft.com/support/legal/sla/)

**ドキュメント:**

-   Azure Active Directory のドキュメント サイト:[Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Azure Active Directory ライブラリ:[Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Office 365 ライブラリ:[Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## 質問がここに含まれていない場合は、どうすればよいですか
[Azure Rights Management の情報とサポート](../Topic/Information_and_Support_for_Azure_Rights_Management.md) に一覧表示されているリンクとリソースを使用します。

さらに、FAQ がエンドユーザー向けに用意されています。

-   [Windows 用 Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn467883)

-   [モバイル プラットフォームと Mac プラットフォームのための Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248)

-   [ドキュメント追跡の FAQ](http://go.microsoft.com/fwlink/?LinkId=523977)

この FAQ ページは定期的に更新されます。新しい情報は [Microsoft Rights Management (RMS) Team](http://blogs.technet.com/b/rms/) ブログ上の月次のドキュメント更新発表に一覧表示されます。

> [!TIP]
> ブログの [docs タグ](http://blogs.technet.com/b/rms/archive/tags/docs/)を使用すると、ドキュメントのお知らせを簡単に見つけることができます。

## 参照
[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)


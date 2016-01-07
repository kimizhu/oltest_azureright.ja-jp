---
description: na
keywords: na
pagetitle: Comparing Azure Rights Management and AD RMS
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
---
# Azure Rights Management と AD RMS を構成する
Active Directory Rights Management  Services (AD RMS) を理解している、または以前にデプロイしたことがある場合、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) と機能や要件を比較するにはどうすればよいかと思われるかもしれません。 次の表を使用して、Azure RMS と AD RMS の機能と利点を並べて比較することができます。 セキュリティに関する比較について質問がある場合は、このトピックの「[署名と暗号化のための暗号化制御](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md#BKMK_CryptographicControls)」セクションを参照してください。

> [!NOTE]
> 簡単に比較できるようにするために、ここでの一部の情報は「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」と同じものを記載しています。[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] のより具体的なサポートおよびバージョン情報については、そのトピックを参照してください。

|[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS)|Active Directory Rights Management Services (AD RMS)|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Exchange Online や SharePoint Online などの Microsoft Online Services および Office 365 で Information Rights Management (IRM) 機能をサポートします。<br /><br />さらに、Exchange Server、SharePoint Server などのオンプレミスの Microsoft サーバー製品、および Windows Server とファイル分類インフラストラクチャ (FCI) を実行するファイル サーバーもサポートします。|Exchange Server、SharePoint Server などのオンプレミスの Microsoft サーバー製品、および Windows Server とファイル分類インフラストラクチャ (FCI) を実行するファイル サーバーもサポートします。|
|組織と任意の組織のユーザー間の暗黙的な信頼関係を有効にします。 これは、ユーザーが [!INCLUDE[o365_1](../Token/o365_1_md.md)] または [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を使用しているか、ユーザーが個人用 RMS にサインアップしているときに、同じ組織または異なる組織のユーザー間で保護されたコンテンツを共有できることを意味します。|信頼関係は、信頼されたユーザー ドメイン (TUD) または Active Directory フェデレーション サービス (AD FS) を使用して作成したフェデレーションによる信頼関係を使用して、2 つの組織間で直接のポイントツーポイントの関係で明示的に定義される必要があります。|
|2 つの既定の権利ポリシー テンプレートが用意されています。これらのテンプレートは、コンテンツのアクセスを組織に制限します。一方のテンプレートは保護されたコンテンツの読み取り専用の表示を提供し、もう一方のテンプレートは保護されたコンテンツの書き込みまたは変更アクセス許可を提供します。<br /><br />ユーザーのサブセットのみが見ることのできる部門テンプレートを含む独自のカスタム テンプレートを作成することもできます。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md)」を参照してください。<br /><br />また、テンプレートで不十分な場合は、独自のアクセス許可セットを定義できます。|既定の権限ポリシー テンプレートがない場合は、作成してから配布する必要があります。 詳細については、「[AD RMS ポリシー テンプレートに関する考慮事項](http://go.microsoft.com/fwlink/?LinkId=154765)」を参照してください。<br /><br />また、テンプレートで不十分な場合は、独自のアクセス許可セットを定義できます。|
|サポートされる Microsoft Office の最小バージョンは Office 2010 であり、このバージョンでは [RMS 共有アプリケーション](http://technet.microsoft.com/library/dn339006.aspx)が必要です。<br /><br />Microsoft Office for Mac:<br /><br />-   Microsoft Office for Mac 2016:サポートされています<br />-   Microsoft Office for Mac 2011:サポートされていません|サポートされる最小バージョンは Microsoft Office is Office 2007 です。<br /><br />Microsoft Office for Mac:<br /><br />-   Microsoft Office for Mac 2016:サポートされています<br />-   Microsoft Office for Mac 2011:サポートされています|
|Windows、Mac コンピューター、モバイル デバイス用の [RMS 共有アプリケーション](https://technet.microsoft.com/library/dn919648%28v=ws.10%29.aspx)をサポートします。<br /><br />また、RMS 共有アプリケーションは次の機能をサポートします。<br /><br />-   別組織のユーザーとの共有。<br />-   電子メール通知。保護された添付ファイルを誰かが開こうとすると、送信者に通知されます。<br />-   ユーザー用のドキュメント追跡サイト。ドキュメントを失効させる機能があります。|Windows、Mac コンピューター、モバイル デバイス用の [RMS 共有アプリケーション](https://technet.microsoft.com/library/dn919648%28v=ws.10%29.aspx)をサポートします。 ただし、別組織のユーザーとの共有、電子メール通知、ドキュメント追跡サイトとユーザーがドキュメントを失効させる機能はサポートされていません。|
|[RMS 共有アプリケーションを使用する場合、ネイティブ保護または一般的な保護を使用して](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)、すべてのファイルの種類を保護できます。<br /><br />他のアプリケーションについては、[クライアント機能一覧](https://technet.microsoft.com/library/dn655136.aspx)をご覧ください。|[RMS 共有アプリケーションを使用する場合、ネイティブ保護または一般的な保護を使用して](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)、すべてのファイルの種類を保護できます。<br /><br />他のアプリケーションについては、[クライアント機能一覧](https://technet.microsoft.com/library/dn655136.aspx)をご覧ください。|
|Windows クライアントのサポートされる最小バージョンは Windows 7 です。|Windows クライアントのサポートされる最小バージョンは Windows Vista Service Pack 2 です。|
|モバイル デバイスのサポートには、Windows Phone、Android、iOS、および Windows RT が含まれます。<br /><br />Exchange ActiveSync IRM を使用する電子メール サポートが、このプロトコルをサポートするすべてのモバイル デバイス プラットフォーム上でもサポートされます。|モバイル デバイスのサポート対象には、Windows Phone、Android、iOS、Windows RT が含まれます。モバイル デバイスを使用するには、[Active Directory Rights Management サービスのモバイル デバイス拡張機能](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341)が必要です。<br /><br />Exchange ActiveSync IRM を使用する電子メール サポートが、このプロトコルをサポートするすべてのモバイル デバイス プラットフォーム上でサポートされます。|
|コンピューターとモバイル デバイス用の多要素認証 (MFA) をサポートします。<br /><br />詳細については、「[多要素認証 (MFA) と Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_MFA)」の「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」セクションを参照してください。|IIS が証明書を要求するように構成されている場合は、スマート カード認証をサポートします。|
|追加の構成なしで Cryptographic Mode 2 をサポートします。これによりキー長と暗号化アルゴリズムのセキュリティが強化されます。<br /><br />詳細については、このトピックの「[署名と暗号化のための暗号化制御](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md#BKMK_CryptographicControls)」セクションと、「[AD RMS の暗号化モード](http://go.microsoft.com/fwlink/?LinkId=266659)」を参照してください。|既定で Cryptographic Mode 1 をサポートし、セキュリティを強化するために Cryptographic Mode 2 をサポートするには追加の構成が必要です。<br /><br />詳細については、このトピックの「[署名と暗号化のための暗号化制御](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md#BKMK_CryptographicControls)」セクションと「[AD RMS の Cryptographic Mode (英語)](http://go.microsoft.com/fwlink/?LinkId=266659)」を参照してください。|
|AD RMS から、および必要な場合は AD RMS への、移行のサポート:<br /><br />-   [AD RMS から Azure Rights Management への移行](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md)<br />-   [Azure Rights Management の使用停止と非アクティブ化](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md)|Azure RMS から、および Azure RMS への移行のサポート:<br /><br />-   [Azure Rights Management の使用停止と非アクティブ化](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md)<br />-   [AD RMS から Azure Rights Management への移行](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md)|
|コンテンツを保護するには RMS ライセンスが必要です。 Azure RMS によって保護されたコンテンツを使用するのに、RMS ライセンスは必要ありません (別の組織のユーザーも含みます)。<br /><br />詳細については、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」の「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションを参照してください。|AD RMS によってコンテンツを保護し、保護されたコンテンツを使用するには、RMS ライセンスが必要です。<br /><br />AD RMS のライセンスの概要については、「[Client Access Licenses and Management Licenses (クライアント管理ライセンスとアクセス ライセンス)](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx)」を参照してください。具体的な情報については、マイクロソフト パートナーまたはマイクロソフトの担当者に問い合わせてください。|

## <a name="BKMK_CryptographicControls"></a>署名と暗号化のための暗号化制御
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] は常に、すべての公開キーの暗号化に RSA 2048 を使用し、署名操作に SHA 256 を使用します。 これに対し、AD RMS は、RSA 1024 および RSA 2048 をサポートし、署名操作用に SHA 1 または SHA 256 をサポートします。

[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] と AD RMS はどちらも対称暗号化に AES 128 を使用します。

テナント キーが Microsoft によって作成および管理されるか (既定)、テナント キーを自分で管理する場合 (BYOK と呼ばれます)、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] は、FIPS 140-2 と互換性があります。 テナント キーの管理の詳細については、「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」を参照してください。

## 参照
[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)


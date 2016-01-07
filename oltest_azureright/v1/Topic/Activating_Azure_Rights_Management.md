---
description: na
keywords: na
pagetitle: Activating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
---
# Rights Management をアクティブにする
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) をアクティブにすると、この情報保護ソリューションをサポートするアプリケーションとサービスを使用して組織の重要なデータの保護を開始できます。 管理者は、組織が所有する保護されたファイルや電子メールを管理および監視することもできます。 Office、SharePoint、および Exchange の中で Information Rights Management (IRM) 機能を使用して機密ファイルを保護するには、あらかじめ [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] を有効にする必要があります。

サービスをアクティブ化する前に Azure Rights Management の詳細を知りたい場合 (たとえば、解決するビジネス上の問題、一般的な用途、そのしくみなど)、「[Azure Active Directory Rights Management の概要](../Topic/What_is_Azure_Rights_Management_.md)」を参照してください。

> [!IMPORTANT]
> [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] をアクティブ化する前に、組織に [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスを含むサービス プランがあることを確認します。 ない場合は、Azure RMS をアクティブにすることはできません。
> 
> 詳細については、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」の「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションを参照してください。

Azure RMS をアクティブ化した後は、組織内のすべてのユーザーはファイルに情報保護を適用でき、すべてのユーザーは Azure RMS で保護されているファイルを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、このトピックの「[段階的デプロイのオンボーディング コントロールの構成](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls)」セクションを参照してください。

## Rights Management のアクティブ化
[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] をアクティブにするには、以下の方法のうちのいずれか 1 つを使用します。

> [!TIP]
> また、[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] をアクティブにするには、Windows PowerShell コマンドレットの [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) も使用できます。

#### Office 365 管理センターから Rights Management をアクティブにするには

1.  Rights Management が含まれている Office 365 プランにサインアップした後、Office 365 のデプロイの管理者である[職場または学校のアカウントで Office 365 にサインイン](https://portal.office.com/)します。

2.  Office 365 管理センターが自動的に表示されない場合は、左上のアプリケーション ランチャー アイコンを選択し、[**管理**] を選択します。 [**管理**] タイルは、Office 365 管理者に対してのみ表示されます。

    > [!TIP]
    > 管理センターのヘルプについては、「[Office 365 管理センターについて - 管理者向けヘルプ](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)」を参照してください。

3.  左ペインで、**[サービス設定]** を展開します。

4.  [**Rights Management**] をクリックします。

    > [!NOTE]
    > このオプションが表示されない場合は、サービス プランまたは製品バージョンが Rights Management に対応していないか、Rights Management をサポートするアップグレードが済んでいないことが考えられます。
    > 
    > サポート対象を確認するには、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」の「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションの情報を使用します。 サービス プランまたは製品バージョンが対応しているにもかかわらず Rights Management オプションが表示されない場合、サービスのアップグレードが済んでいないことが考えられます。 この問題でサポートが必要な場合は、[askipteam](mailto:askipteam@microsoft.com?subject=I%20cannot%20activate%20RMS) 宛てに電子メール メッセージを送信してください。

5.  [**RIGHTS MANAGEMENT**] ページで、[**管理**] をクリックします。

6.  **[RIGHTS MANAGEMENT]** ページで、**[アクティブ化]** をクリックします。

7.  [**Rights Management をアクティブ化しますか?**] というメッセージが表示されたら、[**アクティブ化**] をクリックします。

[**Rights Management はアクティブ化されています**] というテキストと、非アクティブ化するオプションが表示されます。

#### Azure クラシック ポータルから Rights Management をアクティブ化するには

1.  Azure アカウントにサインアップした後、[Azure クラシック ポータルにサインイン](http://go.microsoft.com/fwlink/p/?LinkID=275081)します。

2.  左ペインで、[**ACTIVE DIRECTORY**] をクリックします。

3.  [**Active Directory**] ページで、[**RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択して、[**アクティブ化**] をクリックし、操作を確定します。

    > [!NOTE]
    > アクティブ化エラーとなった場合は、原因として、サービス プランまたは製品バージョンが [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] をサポートできないことが考えられます。
    > 
    > RMS のサポートを確認するには、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」の「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションの情報を使用します。 この問題でサポートが必要な場合は、[askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS) 宛てに電子メール メッセージを送信してください。

これで、[**Rights Management のステータス**] に [**アクティブ**] と表示され、[**アクティブ化**] オプションが [**非アクティブ化**] に置き換えられます。

### Azure クラシック ポータルでの Rights Management のステータス値および説明
[**アクティブ**] ステータス (Rights Management サービスが有効化され、使用できる状態にあることを示す) の他に、[**非アクティブ**]、[**利用不可**]、または [**許可されていません**] が表示される場合もあります。

|ステータス値|説明|
|----------|------|
|**Active**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] は有効化され、使用できる様態にあります。|
|**非アクティブ**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] は、無効になっているので、組織がファイルを保護できるようにするにはアクティブ化する必要があります。|
|**利用不可**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスはダウンしています。 後でもう一度やり直してください。|
|**許可されていません**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスのステータスを表示する権限がありません。 たとえば、アカウントがロックアウトされているか、または選択したテナントのグローバル管理者になっていません。|

## <a name="BKMK_OnboardingControls"></a>段階的デプロイのオンボーディング コントロールの構成
すべてのユーザーが Azure RMS を使用してすぐにファイルを保護できるようにしたくない場合は、[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) Windows PowerShell コマンドを使用してユーザー オンボーディング コントロールを構成できます このコマンドを実行するのは、Azure RMS をアクティブ化する前と後のどちらでもかまいません。

> [!IMPORTANT]
> このコマンドを使用するには、バージョン **2.1.0.0** 以降の [Azure RMS Windows PowerShell モジュール](http://go.microsoft.com/fwlink/?LinkId=257721)が必要です。
> 
> です。インストールされているバージョンを確認するには: **(Get-Module aadrm –ListAvailable).Version**

たとえば、テストのために最初は “IT department” グループ (オブジェクト ID が fbb99ded-32a0-45f1-b038-38b519009503) の管理者だけがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
この構成オプションでは、グループを指定する必要があります。個々 のユーザーを指定することはできません。

または、Azure RMS の使用を適切にライセンスされているユーザーのみがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
これらのオンボーディング コントロールを使用するときは、保護されたコンテンツを組織内のすべてのユーザーがいつでも使用できますが、コンテンツを保護できるのは組織内の一部のユーザーのみとなり、それ以外のユーザーは情報保護を自分でクライアント アプリケーションから適用することはできません。 たとえば、そのようなユーザーの Office クライアントには、Azure RMS がアクティブになると自動的に公開される既定のテンプレートや管理者が構成したカスタム テンプレートは表示されません。  Exchange などのサーバー側のアプリケーションには、RMS と統合された場合に同じ結果を達成するための、独自のユーザー単位コントロールを実装する機能があります。

## 次の手順
これで組織に対して [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] がアクティブになったので、[Azure Rights Management の展開ロードマップ](../Topic/Azure_Rights_Management_Deployment_Roadmap.md)を使用して、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] をユーザーおよび管理者にロールアウトする前にその他の構成手順が必要かどうかを判断します。 たとえば、[カスタム テンプレート](http://technet.microsoft.com/library/dn642472.aspx)を使用してユーザーが簡単に情報保護をファイルに適用できるようにする、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を使用するために [RMS コネクタ](http://technet.microsoft.com/library/dn375964.aspx)をインストールしてオンプレミス サーバーに接続する、すべてのデバイスですべてのファイルの種類の保護をサポートする [Rights Management 共有アプリケーション](http://technet.microsoft.com/library/jj585031.aspx)をデプロイする、などが考えられます。 Exchange Online や SharePoint Online などの Office サービスの Information Rights Management (IRM) 機能を使用するには、あらかじめ追加の構成手順が必要です。 ただし、その他に実行が必要な構成手順がない場合は、「[Azure Rights Management を使用する](../Topic/Using_Azure_Rights_Management.md)」を参照してください。ここに記載されている運用ガイダンスは、組織への適切な展開に役立ちます。

アプリケーションと [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] の動作については、「[アプリケーションで Azure Rights Management をサポートする方法](../Topic/How_Applications_Support_Azure_Rights_Management.md)」を参照してください。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


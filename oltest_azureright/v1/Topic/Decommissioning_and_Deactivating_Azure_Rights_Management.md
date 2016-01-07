---
description: na
keywords: na
pagetitle: Decommissioning and Deactivating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
---
# Azure Rights Management の使用停止と非アクティブ化
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) を使用すると、組織がコンテンツを保護するかどうかをいつでも制御できます。また、この情報保護ソリューションの使用をやめた場合でも、以前に保護されていたコンテンツから締め出されることはありません。 以前に保護されていたコンテンツに引き続きアクセスする必要がない場合、サービスを無効にして Azure Rights Management のサブスクリプションの有効期限を終わらせることができます。 たとえば、これは、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を運用環境にデプロイする前のテストが完了した場合も該当します。

ただし、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を運用環境にデプロイした場合、サービスを無効にする前に Azure Rights Management テナント キーのコピーを用意し、サブスクリプションの期限が切れる前にサービスを無効にします。これにより、サービスを無効にした後でも、Azure Rights Management で保護されていたコンテンツに引き続きアクセスできるようになります。 BYOK (Bring Your Own Key) を使用し、HSM で独自のキーを生成し管理している場合、Azure Rights Management テナント キーが既に与えられています。 ただし、そのキーが Microsoft により管理されていた場合 (既定) は、[Azure Rights Management テナント キーに対する操作](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md)トピックでテナント キーのエクスポートの手順をご確認ください。

> [!TIP]
> サブスクリプションの有効期限が切れた後も、延長された期間中、Azure Rights Management テナントでコンテンツを利用できます。 ただし、テナント キーをエクスポートすることはできなくなります。

Azure Rights Management テナント キーがある場合は、オンプレミスで Rights Management (AD RMS) をデプロイし、信頼された発行ドメイン (TPD) としてテナント キーをインポートできます。 Azure Rights Management デプロイメントは次の方法で使用停止できます。

|条件|… 手順|
|------|--------|
|すべてのユーザーに Rights Management を引き続き利用させたいが、Azure RMS ではなくオンプレミス ソリューションを利用する場合|この変更後に保護されたコンテンツを既存ユーザーが使用するときにユーザーをオンプレミス デプロイメントに移動させるには、[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) コマンドレットを使用します。 ユーザーが保護されたコンテンツを使用する際に、自動的に AD RMS インストールを利用するようになります。<br /><br />この変更前に保護されたコンテンツをユーザーが使用できるようにするには、RMS クライアント デプロイメント ノートの[サービスの検出](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx)セクションの説明に従って Office 2016 または Office 2013 の **LicensingRedirection** レジストリ キーを利用、または「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」 の説明に従って Office 2010 の **LicenseServerRedirection** レジストリ キーを利用して、クライアントをオンプレミス デプロイメントにリダイレクトします。|
|Rights Management テクノロジの使用を完全に停止する場合|指定の管理者に[スーパー ユーザー権限](https://technet.microsoft.com/library/mt147272.aspx)を与え、その管理者に [RMS 保護ツール](http://www.microsoft.com/en-us/download/details.aspx?id=47256)を提供します。<br /><br />この管理者はこのツールを利用して、Azure Rights Management で保護されていたフォルダーのファイルを一括で復号できます。これにより、ファイルの保護が解除され、Azure RMS や AD RMS などの Rights Management テクノロジがなくても読み取ることができるようになります。 このツールは Azure RMS と AD RMS の両方に対応します。Azure RMS を無効にする前または後に、あるいは前後で処理を組み合わせて、ファイルを復号できます。|
|Azure RMS で保護されていたファイルの一部を特定できないか、読み取れなかった保護ファイルを自動的にユーザーが読み取れるようにする場合|RMS クライアント デプロイメント ノートの[サービスの検出](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx)セクションの説明に従って Office 2016 と Office 2013 の **LicensingRedirection** レジストリ キーを利用するか、または「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」 の説明に従って Office 2010 の **LicenseServerRedirection** レジストリ キーを利用して、すべてのクライアント コンピューターにレジストリ設定をデプロイします。<br /><br />また、「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って、**DisableCreation** を **1** に設定し別のレジストリ設定をデプロイして、ユーザーが新しいファイルを保護できないようにします。|
|読み取れなかったファイルに、制御された手動回復サービスを実行する場合|データ回復グループの指定ユーザーに[スーパー ユーザー権限](https://technet.microsoft.com/library/mt147272.aspx)を与え、それらのユーザーに [RMS 保護ツール](http://www.microsoft.com/en-us/download/details.aspx?id=47256)を提供し、標準ユーザーに要求されたときにそれらのユーザーがファイルの保護を解除できるようにします。<br /><br />また、すべてのコンピューターで、「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って、**DisableCreation** を **1** に設定して、レジストリ設定をデプロイし、ユーザーが新しいファイルを保護できないようにします。|
この表に記載された各手順の詳細については、以下のリソースをご覧ください。

-   AD RMS とデプロイメントの参照に関する詳細については、「[Active Directory Rights Management サービスの概要](https://technet.microsoft.com/library/hh831364.aspx)」をご覧ください。

-   Azure RMS テナント キーを TPD ファイルとしてインポートする方法については、「[信頼された発行ドメインを追加する](https://technet.microsoft.com/library/cc771460.aspx)」をご覧ください。

-   Azure RMS 用の Windows PowerShell モジュールをインストールし、移行 URL を設定する方法については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」をご覧ください。

組織の Azure RMS を無効にする用意ができたら、次の手順に従います。

## Rights Management の非アクティブ化
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を非アクティブ化するには、次のいずれかの手順を使用します。

> [!TIP]
> [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] を非アクティブ化にするには、Windows PowerShell コマンドレットの [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) も使用できます。

#### Office 365 管理センターから Rights Management を非アクティブ化するには

1.  Office 365 デプロイの管理者である[職場または学校のアカウントで Office 365 にサインイン](https://portal.office.com/)します。

2.  Office 365 管理センターが自動的に表示されない場合は、左上のアプリケーション ランチャー アイコンを選択し、[**管理**] を選択します。 [**管理**] タイルは、Office 365 管理者に対してのみ表示されます。

    > [!TIP]
    > 管理センターのヘルプについては、「[Office 365 管理センターについて - 管理者向けヘルプ](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)」を参照してください。

3.  左ペインで、**[サービス設定]** を展開します。

4.  [**Rights Management**] をクリックします。

5.  [**Rights Management**] ページで、[**管理**] をクリックします。

6.  [**Rights Management**] ページで、[**非アクティブ化**] をクリックします。

7.  [**Rights Management を非アクティブ化しますか?**] というメッセージが表示されたら、[**非アクティブ化**] をクリックします。

[**Rights Management がアクティブ化されていません**] というテキストとアクティブ化するオプションが表示されます。

#### Azure ポータルから Rights Management を非アクティブ化するには

1.  [Azure クラシック ポータル](http://go.microsoft.com/fwlink/p/?LinkID=275081)にサインインします。

2.  左ペインで、[**ACTIVE DIRECTORY**] をクリックします。

3.  [**active directory**] ページで、[**RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択して、[**非アクティブ化**] をクリックし、操作を確定します。

これで、[**Rights Management のステータス**] に [**非アクティブ**] と表示され、[**非アクティブ化**] オプションが [**アクティブ化**] に置き換えられます。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


---
description: na
keywords: na
pagetitle: Configuring Super Users for Azure Rights Management and Discovery Services or Data Recovery
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
---
# Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成
Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) のスーパー ユーザー機能により、承認されたユーザーとサービスは、Azure RMS によって保護されている組織のデータをいつでも読み取り、検査することができます。 さらに必要に応じて、保護を削除したり、以前に適用されていた保護を変更したりできます。 スーパー ユーザーは常に、組織の RMS テナントによって付与されたすべての使用ライセンスに対して完全な所有者権限を持ちます。 この機能は “データに対する推論” と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。 たとえば、次のいずれかのシナリオでこの機能を使用することがあります。

-   退職した従業員によって保護されたファイルを読み取る必要がある。

-   IT 管理者は、ファイルに対して構成されている現在の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

-   Exchange Server で、検索操作のためにメールボックスにインデックスを付ける必要がある。

-   既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

-   監査、法律、またはその他のコンプライアンス上の理由で、ファイルを一括で復号化する必要がある。

既定で、スーパー ユーザー機能は無効であり、このロールはどのユーザーにも割り当てられていません。 これは、Exchange に Rights Management コネクタを構成すると自動的に有効にされますが、Exchange Online、SharePoint Online、または SharePoint Server を実行する標準的なサービスには必要ありません。

スーパー ユーザー機能を手動で有効にする必要がある場合は、Windows PowerShell コマンドレット [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) を使用します。次に必要に応じて [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) コマンドレットを使用して、ユーザー (またはサービス アカウント) を割り当てます。 組織では、1 つまたは複数のスーパー ユーザーを使用できます。ただし、ユーザーは別々に追加する必要があり、グループでの追加はサポートされていません。

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。

スーパー ユーザー機能のセキュリティ ベスト プラクティス:

-   Office 365 または Azure RMS テナントのグローバル管理者が割り当てられている管理者、または [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) コマンドレットを使用して、GlobalAdministrator ロールが割り当てられている管理者を制限し、監視します。 これらのユーザーは、スーパー ユーザー機能を有効にし、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができ、組織で保護するすべてのファイルを複合化できます。

-   スーパー ユーザーとして割り当てられたユーザーおよびサービス アカウントを表示するには、[Get-AadrmSuperUser コマンドレット](https://msdn.microsoft.com/library/azure/dn629408.aspx)を使用します。  すべての管理アクションと同様に、スーパー機能の有効化や無効化、およびスーパー ユーザーの追加や削除はログに記録され、[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) コマンドを使用して監査できます。 スーパー ユーザーがファイルを復号化すると、この操作はログに記録され、[使用状況ログ](https://technet.microsoft.com/library/dn529121.aspx)で監査できます。

-   日常的なサービスでスーパー ユーザー機能を必要としない場合は、必要なときにのみ有効にし、[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) コマンドレットを使用して、再度無効にします。

次のログの抽出に、Get-AadrmAdminLog コマンドレットの使用によるいくつかのエントリの例を示します。 この例では、Contoso 社の管理者は、スーパー ユーザー機能が無効になっていることを確認し、スーパー ユーザーとして Richard Simone を追加します。Richard が Azure RMS 用に構成された唯一のスーパー ユーザーであることを確認してから、Richard は退職した従業員によって保護されたいくつかのファイルを復号化できるようにスーパー ユーザー機能を有効にします。

`2015-08-01T18:58:20	admin@contoso.com	GetSuperUserFeatureState	Passed	Disabled`
`2015-08-01T18:59:44	admin@contoso.com	AddSuperUser -id rsimone@contoso.com	Passed	True`
`2015-08-01T19:00:51	admin@contoso.com	GetSuperUser	Passed	rsimone@contoso.com`
`2015-08-01T19:01:45	admin@contoso.com	SetSuperUserFeatureState -state Enabled	Passed	True`

## <a name="BKMK_RMSProtectionModule"></a>スーパー ユーザーのスクリプト作成オプション
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] のスーパー ユーザーが割り当てられているだれかが、複数の場所で、複数のファイルから保護を削除することが必要になる場合がよくあります。 これは手動で行うことができますが、スクリプト化するとより効率的に (そしてより確実に) 行うことができます。 そのためには、[RMS 保護ツールをダウンロード](http://www.microsoft.com/en-us/download/details.aspx?id=47256)します。 次に、 [Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) コマンドレットを使用し、必要に応じて、[Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) コマンドレットも使用します。

> [!IMPORTANT]
> RMS 保護ツールは、スーパー ユーザーが回復の目的でファイルの保護を一括解除するために設計されていますが、現在のバージョンのツールは Azure RMS のユーザー認証をサポートしていません。 この制限が解決されるまでは、ファイルから保護を削除する前に、Azure RMS による認証に、サービス プリンシパル アカウントを使用する必要があります。  詳細および手順については、「[about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/azure/mt433202.aspx)」を参照してください。

これらのコマンドレットの詳細については、「[RMS 保護コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)」を参照してください。

> [!NOTE]
> RMS 保護ツールに付属する RMSProtection Windows PowerShell モジュールはメインの [Azure Rights Management 用 Windows PowerShell モジュール](https://technet.microsoft.com/library/jj585027.aspx)とは異なり、それを補足するものです。 これは、Azure RMS と AD RMS の両方をサポートします。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


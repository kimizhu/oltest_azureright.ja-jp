---
description: na
keywords: na
pagetitle: Administering Azure Rights Management by Using Windows PowerShell
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
---
# Windows PowerShell を使用した Azure Rights Management の管理
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] は、[!INCLUDE[o365_2](../Token/o365_2_md.md)] 管理センターまたは Azure クラシック ポータルを使用してアクティブ化できますが、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールを使用することもできます。

[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] のアクティブ化が完了したら、それ以降のサービス管理作業は必要ありません。 ただし、高度な構成シナリオでは、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールの使用が必要になる場合があります。 次の表に、Windows PowerShell を使用する高度な構成シナリオの一部を示します。 使用可能なコマンドレットの完全なリストと各コマンドレットの詳細情報については、「[Azure Rights Management コマンドレット](http://msdn.microsoft.com/library/azure/dn629398.aspx)」を参照してください。

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] 用の Windows PowerShell モジュールをインストールする必要がある場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。

Azure RMS と AD RMS の両方をサポートする補完的な Windows PowerShell モジュールである **RMSProtection** もあります。 たとえば、このモジュールでは複数ファイルの保護と、複数ファイルからの保護の削除をサポートしており、フォルダーに含まれるすべてのファイルを包括的に保護できます。 詳細については、「[スーパー ユーザーのスクリプト作成オプション](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md#BKMK_RMSProtectionModule)」の「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md)」セクションを参照してください。

|実行するタスク|使用するコマンドレット|
|-----------|---------------|
|オンプレミスの Rights Management (AD RMS または Windows RMS) から [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] に移行する。|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスに接続する、またはこのサービスから切断する。|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|独自のテナント キーを生成および管理する - BYOK (Bring Your Own Key) シナリオ。|[Add-AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスをアクティブ化または非アクティブ化する。|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Azure Rights Management のドキュメント管理サイトをアクティブ化または非アクティブ化する。|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Azure Rights Management の段階的なデプロイメントのためのオンボード コントロールを構成する。|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|組織の権利ポリシー テンプレートを作成および管理する。|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|インターネット接続を利用しないで、組織によって保護されたコンテンツにアクセスできる最大日数を構成します (使用ライセンスの有効期間)。|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] のスーパー ユーザー機能を管理する。|[Enable-AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get–AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629405.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスの管理が許可されているユーザーとグループを管理する。|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629424.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] 管理タスクのログを取得する。|[Get-AadrmAdminLog](http://msdn.microsoft.com/library/azure/dn629430.aspx)|
|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] の使用状況ログを記録および分析する。|[Enable-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629421.aspx)<br /><br />[Get-AadrmUsageLog](http://msdn.microsoft.com/library/azure/dn629401.aspx)<br /><br />[Get-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629425.aspx)<br /><br />[Get-AadrmUsageLogLastCounterValue](http://msdn.microsoft.com/library/azure/dn629423.aspx)<br /><br />[Get-AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629419.aspx)<br /><br />[Set-AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629426.aspx)<br /><br />[Disable-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629404.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスの現在の構成を表示する。|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|組織を [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] からオンプレミスの AD RMS デプロイに移行する。|[Set-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

## 参照
[Azure Rights Management](../Topic/Azure_Rights_Management.md)


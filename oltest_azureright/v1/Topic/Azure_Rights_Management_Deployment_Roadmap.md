---
description: na
keywords: na
pagetitle: Azure Rights Management Deployment Roadmap
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
---
# Azure Rights Management の展開ロードマップ
組織の Azure Rights Management (Azure RMS) を準備、実装、管理するには、次の手順に沿います。

ただし、運用環境に展開せずに、簡単に Azure RMS を試す場合は、「[Azure Rights Management のクイック スタート チュートリアル](../Topic/Quick_Start_Tutorial_for_Azure_Rights_Management.md)」を参照してください。

> [!IMPORTANT]
> 次の手順を実行する前に、「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」を確認してください。

## 手順 1:Azure Rights Management を含むサブスクリプションがあることを確認します。
[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] を含むサブスクリプションのタイプは複数あります。 「[Azure Rights Management の要件](../Topic/Requirements_for_Azure_Rights_Management.md)」トピックの「[Azure RMS をサポートするクラウド サブスクリプション](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions)」セクションを参照し、「[Rights Management Services (RMS) の提供内容の比較](https://technet.microsoft.com/dn858608)」の表を参照して、組織で使用する機能がサブスクリプションに含まれていることを確認します。

## 手順 2:Rights Management を使用するためにテナント アカウントを準備する
[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] を使用する前に、次の準備を行います。

1.  Azure または Office 365 テナントに、組織のユーザーを認証するのに Azure RMS で使用されるユーザー アカウントとグループが含まれていることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 詳細については、「[Azure Rights Management の準備を行う](../Topic/Preparing_for_Azure_Rights_Management.md)」を参照してください。

2.  マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 現時点では、Exchange Online を使用する場合、BYOK は使用できない点に注意してください。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md)」を参照してください。

3.  インターネットにアクセスできる 1 つ以上のコンピューターで [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] 向けの Windows PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md)」を参照してください。

4.  現在、社内の Rights Management サービスを使用している場合:キー、テンプレート、URL をクラウドに移行する統合を実行します。 詳細については、「[AD RMS から Azure Rights Management への移行](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md)」を参照してください。

5.  サービスの使用を開始できるように Rights Management をアクティブ化します。 段階的に展開する必要がある場合、特定のユーザーの使用量を制限するオンボーディング コントロールを構成します。 詳細については、「[Rights Management をアクティブにする](../Topic/Activating_Azure_Rights_Management.md)」を参照してください。

必要に応じて、次の構成を考慮してください。

-   既定の権限ポリシー テンプレートが組織にとって十分でない場合はカスタム テンプレート。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md)」を参照してください。

-   組織での Rights Management の使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management の利用状況をログに記録して分析する](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md)」を参照してください。

## 手順 3:Rights Management 用にアプリケーションとサービスを構成する
アプリケーションの構成には、Rights Management 共有アプリケーションのインストール、SharePoint Online または Exchange Online での Information Rights Management (IRM) 機能の有効化が含まれることがあります。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)」を参照してください。

Azure RMS によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure RMS のスーパー ユーザーとして設定します。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md)」を参照してください。

Azure Rights Management で使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタを展開する](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)」を参照してください。

## 手順 4:権限保護されたコンテンツをパブリッシュおよび使用する
これで、保護されたコンテンツを発行して利用し、組織で Rights Management を使用する方法を記録する準備が整いました。 詳細については、「[Azure Rights Management を使用する](../Topic/Using_Azure_Rights_Management.md)」を参照してください。

## 手順 5:必要に応じてテナント アカウントの Rights Management を管理する
[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] の使用を開始すると、Windows PowerShell の [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] モジュールがスクリプトまたは管理変更の自動化に役立つことがあります。 詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)」を参照してください。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


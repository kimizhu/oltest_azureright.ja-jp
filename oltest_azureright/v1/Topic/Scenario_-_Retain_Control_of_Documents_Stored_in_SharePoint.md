---
description: na
keywords: na
pagetitle: Scenario - Retain Control of Documents Stored in SharePoint
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89
---
# シナリオ- SharePoint に保存されている文書のコントロールを保持する
このセクションには、管理者用の手順と、ユーザーの手順に関するガイダンスが含まれています。この構成の詳細をユーザーに通知する前に、管理者用の手順を完了する必要があります。

## 管理者用の手順
![](../Image/AzRMS_AdminBanner.png)

次の手順に従って、保護されたライブラリを使用して SharePoint に保存されている Office ドキュメントのコントロールを保持するようにします。たとえばドキュメントは、偶発的またはユーザーの故意による漏えいから自動的に保護され、ドキュメントがダウンロードや同期された後でも、コンテンツへのアクセスをブロックすることができます。保護するファイルの例としては、共同作業用の設計文書や企画、成果物などがあります。SharePoint で保護されたライブラリを構成すると、SharePoint 内の Office ファイルは Azure Rights Management によって保護されます。

この手順は、次の一連の状況に適してします。

-   従業員は、Office ドキュメントを使って共有したり、共同作業したりします。

-   ドキュメントには非公開の情報が含まれますが、必ずしも内部使用に限定されるものでもありません。

-   管理者がライブラリ レベルで設定したアクセス許可を、従業員が設定したり変更したりする必要はありません。

## このシナリオの要件
このシナリオを実現するには、次の内容が必要になります。

|Check|要件|詳細情報が必要な場合|
|---------|------|--------------|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Office 365 または Azure Active Directory のアカウントとグループを準備した|[Azure Rights Management の準備を行う](https://technet.microsoft.com/library/jj585029.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Rights Management がアクティブ化されている|[Rights Management をアクティブにする](https://technet.microsoft.com/library/jj658941.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|SharePoint サーバーを使用する場合:RMS コネクタを展開し、SharePoint 用に構成する|[Azure Rights Management コネクタを展開する](https://technet.microsoft.com/library/dn375964.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|SharePoint を IRM と保護されたライブラリ用に構成する|[SharePoint 管理センターにおける Information Rights Management (IRM) の設定](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Information Rights Management をリストまたはライブラリに適用する](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

## ユーザーの手順
保護されたライブラリには、ユーザーが取るべき手順は特にないため、このシナリオではユーザーに説明する必要のある手順はありません。SharePoint の管理者がサイトに設定したアクセス許可に従って、ドキュメントは自動的に保護されます。ただし、どのライブラリが保護されているのか、それによってユーザーによるドキュメント使用がどのように制限されるのかを、ユーザーやヘルプデスクに伝えておく必要があります。たとえば、現在の制限によって、モバイル デバイスではドキュメントを閲覧できるが、編集はできないといった場合があります。

以下は、Azure RMS を使って SharePoint ライブラリを構成した後、関連する部署やチームに送信される標準的なメール通知の一例です。

### ユーザー ドキュメントの例
![](../Image/AzRMS_ExampleBanner.png)

##### IT からのお知らせ：売上の予測とレポート サイトへの変更

-   **売上予測とレポート**の SharePoint サイトは、コラボレーションの安全性向上のため構成が変更されました。今後、このサイトに保存されているスプレッドシートと Word 文書は、直接編集する必要があります。別の場所に保存して後で編集したり、他のユーザーにメールで送信することはできません。モバイル デバイスでの閲覧は可能ですが、編集は Windows コンピューターで行う必要があります。

**サポートが必要な場合は、**

-   ヘルプ デスク helpdesk@vanarsdelltd.com にお問い合わせください。


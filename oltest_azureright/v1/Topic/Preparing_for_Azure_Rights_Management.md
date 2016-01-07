---
description: na
keywords: na
pagetitle: Preparing for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
---
# Azure Rights Management の準備を行う
[!INCLUDE[o365_1](../Token/o365_1_md.md)] または Azure Active Directory のアカウントでクラウド サブスクリプションにサインアップして組織の登録が完了したら、[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] サービスを有効にする準備ができています。

ただし、その前に、次のものが揃っていることを確認してください。

-   手動で作成するか、または Active Directory ドメイン サービス (AD DS) から自動的に作成および同期される、クラウド内のユーザー アカウントおよびグループ。

    オンプレミスのアカウントとグループを同期するとき、すべての属性を同期する必要はありません。 Azure RMS 用に同期する必要がある属性の一覧については、Azure Active Directory のドキュメントのこの [Azure RMS に関するセクション](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectsync-attributes-synchronized/)を参照してください。 デプロイが容易なので [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) を使用してオンプレミスのディレクトリを Azure Active Directory と接続することをお勧めしますが、同じ結果が得られる他のディレクトリ同期方法を使ってもかまいません。

-   Rights Management で使用する、クラウドでのメールが有効なグループ。 組み込みのグループ、または Rights Management を使用するユーザーを含む手動で作成したグループにすることができます。

    Exchange Online がある場合は、Exchange 管理センターを使用して、メールが有効なグループを作成し使用することができます。 AD DS があり、Azure AD と同期している場合は、セキュリティ グループまたは配布グループであるメールが有効なグループを作成して使用できます。

## Rights Management を有効にする
[!INCLUDE[o365_2](../Token/o365_2_md.md)] または Azure AD アカウントにサインアップした時点で、既定では [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] は無効になっています。 組織で [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] を有効にするには、このサービスをアクティブ化する必要があります。 詳細については、「[Rights Management をアクティブにする](../Topic/Activating_Azure_Rights_Management.md)」を参照してください。

## 参照
[Azure Rights Management を構成する](../Topic/Configuring_Azure_Rights_Management.md)


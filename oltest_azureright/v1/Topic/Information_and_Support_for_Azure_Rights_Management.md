---
description: na
keywords: na
pagetitle: Information and Support for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cc73d92-27d6-49ff-a8ab-2fae73519b4b
---
# Azure Rights Management の情報とサポート
Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) の詳細については、以下のリソースを使用してください。

|目的|.. 手順|
|------|---------|
|… 最新の [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] 製品ドキュメントを参照する →|[Azure Rights Management](../Topic/Azure_Rights_Management.md) の TechNet ドキュメント ライブラリを使用します|
|… ドキュメントに関するフィードバックを提供する、またはドキュメントについて質問する →|[askipteam](mailto:%20askipteam@microsoft.com?subject=Documentation%20feedback) に電子メールを送信します|
|… 製品グループからの Rights Management に関するツイートおよびドキュメントの更新に関する発表を受け取る →|Microsoft Rights Management チームのリーダーである Dan Plastina をフォローします。[Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) を参照してください|
|…[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] の評価版を取得する →|[30 日間の無料評価版にサインアップ](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)|
以下のセクションでは、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] に関する追加情報を提供します。

-   [ドキュメント ライブラリを検索する](../Topic/Information_and_Support_for_Azure_Rights_Management.md#BKMK_SearchTips)

-   [ドキュメントのダウンロード](../Topic/Information_and_Support_for_Azure_Rights_Management.md#BKMK_Download)

-   [Rights Management 製品グループ ブログ](../Topic/Information_and_Support_for_Azure_Rights_Management.md#BKMK_ProductGroupBlog)

-   [サポート オプションとコミュニティ リソース](../Topic/Information_and_Support_for_Azure_Rights_Management.md#BKMK_SupportOptions)

## <a name="BKMK_SearchTips"></a>ドキュメント ライブラリを検索する
[この範囲を指定した検索クエリを使用して](http://www.bing.com/search?q=%28"Rights%20Management"%29%20site:technet.microsoft.com/library%20meta:search.MSCategory%28jj619159%29)
      [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] のみを対象にして TechNet ライブラリのドキュメントを検索できます。

クエリの検索結果には、Active Directory Rights Management Services (AD RMS) または Windows Rights Management に関する結果、またはコミュニティ リソースは含まれません。 URL 内の文字列 “Rights Management” を独自の検索文字列に置き換えることで検索結果をさらに絞り込むことができます。

### 検索の例
[この検索クエリを使用して](http://www.bing.com/search?q=%28"Rights%20Management"%29%20site:technet.microsoft.com/library%20meta:search.MSCategory%28jj619159%29) し、次の例を使用して、検索をカスタマイズします。

-   1 つの検索文字列: 検索文字列 **RMS コネクタ**を含むトピックを検索するには、**“Rights Management”** を **"RMS コネクタ"** に置き換えます。

    ```
    ("RMS connector") site:technet.microsoft.com/library meta:search.MSCategory(jj619159)
    ```

-   検索文字列の組み合わせ: 検索文字列 **Exchange** と **SharePoint** を含むトピックを検索するには、**AND** 演算子を使用します。

    ```
    ("Exchange") AND ("SharePoint") site:technet.microsoft.com/library meta:search.MSCategory(jj619159)
    ```

-   代替の検索文字列: 検索文字列 **Exchange** または **SharePoint** を含むトピックを検索するには、**OR** 演算子を使用します。

    ```
    ("Exchange" OR "SharePoint") site:technet.microsoft.com/library meta:search.MSCategory(jj619159)
    ```

-   除外検索文字列: 検索文字列 **Exchange** を含むトピックを検索し、**SharePoint** に関するトピックを除外するには、**NOT** 演算子を使用します。

    ```
    ("Exchange)" NOT ("SharePoint") site:technet.microsoft.com/library meta:search.MSCategory(jj619159)
    ```

### 検索のヒント
次の検索のヒントは、必要な情報を見つけるために役立ちます。

-   公式ドキュメントを検索している場合は、コミュニティ コンテンツに見られる非公式な用語や略語ではなく、ユーザー インターフェイス (UI) や TechNet ドキュメントの用語と一致する検索用語を使用します。 たとえば、"AADRMS" やこのクラウド サービスの他の非公式な略語ではなく、"Azure Rights Management" を検索します。 “RMS” はよく見聞きする単語ですが、完全な名前は Rights Management サービスなので、公式ドキュメントを探しているときは、RMS ではなく “Rights Management” を検索してみてください。[Azure Rights Management の用語](../Topic/Terminology_for_Azure_Rights_Management.md) を使用して、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] に固有な公式用語を確認することができます。

-   TechNet のページ上で検索するときには (Ctrl + F キーを押し、**[検索]** ボックスに検索用語を入力します)、折りたたまれたセクション内のテキストは結果から除外されます。 折りたたまれたセクション内のテキストを検索するには、ページを検索する前にセクションを展開します。 これを行うには、ページの上部にある **[すべて展開]** ボタンをクリックするか、任意の折りたたまれたセクションをダブルクリックします。 すべてのセクションが展開されていると、ページの検索でそのページのすべてのセクションが検索されます。

-   可能な場合は常に、ダウンロードしたドキュメントでなく、TechNet ライブラリ オンラインを使用します。 TechNet ライブラリ オンラインには最新の情報が含まれており、ダウンロードしたドキュメントには検索している情報が含まれていない場合や、修正や追加情報がオンラインに掲示されている場合があります。

-   ローカルに保存されているドキュメントの方が早く簡単に検索できる場合は、TechNet で複数のトピックを選択して、それらをローカルに保存することができます。 詳細については、次のセクションを参照してください。

## <a name="BKMK_Download"></a>ドキュメントのダウンロード
TechNet からページをダウンロードしてローカルに保存することができます。たとえば、PDF ファイルをノート パソコン、タブレット、または携帯電話に保存して、インターネットに接続されていないときに読むことができます。 または、それらの情報に自分で注釈を付けて印刷します。 この方法を使用すると、特定のタスクのセットやエンドツーエンドのシナリオに必要なトピックをグループにまとめることで、独自のホワイト ペーパーやプロジェクト ドキュメントを効果的に作成できます。

この方法は、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] だけでなく TechNet のすべてのドキュメント ライブラリで使用できます。

#### TechNet からドキュメントをダウンロードするには:

1.  TechNet にサインインします。

2.  ローカルに保存するページの一番上で、**[エクスポート]** (**[印刷]** の横にあります) をクリックします。

    次に表示される **[複数のページのセットのエクスポート]** バナーを使用して、保存するページを追加および削除することができます。

3.  **[ページの管理]** をクリックしてエクスポートします。

詳細については、バナーの **[ヘルプ]** をクリックしてください。

> [!NOTE]
> TechNet 上の情報は頻繁に更新されるので、できる限りオンライン版を使用して、最新の情報を入手してください。
> 
> [Microsoft Rights Management (RMS) チーム ブログと docs タグ](http://blogs.technet.com/b/rms/archive/tags/docs/)の毎月のドキュメントに関するお知らせを参照すると、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] の以前にダウンロードしたトピックが改訂されたかどうかと、変更内容を確認できます。

## <a name="BKMK_ProductGroupBlog"></a>Rights Management 製品グループ ブログ
Rights Management 製品グループは、[Microsoft Rights Management (RMS) チーム ブログ](http://blogs.technet.com/b/rms/)を使用して、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], AD RMS や関連する技術の技術情報と新規情報を提供しています。 これらのブログには、製品ドキュメントの補足やサポート情報が投稿されます。

> [!TIP]
> Azure RMS または AD RMS 用のアプリケーションを開発している場合、[Active Directory Rights Management Services (AD RMS) 開発者のコーナー ブログ](http://blogs.msdn.com/b/rms/)もお勧めです。

## <a name="BKMK_SupportOptions"></a>サポート オプションとコミュニティ リソース
次のリンクは、サポートおよびトラブルシューティングのオプションとコミュニティ リソースに関する情報を提供します。

-   [RMS アナライザー ツール](http://www.microsoft.com/en-us/download/details.aspx?id=46437)

-   [Yammer:Microsoft Rights Management (RMS)](http://www.yammer.com/AskIPTeam)

-   [フォーラム:Microsoft RMS (クラウド)](https://social.technet.microsoft.com/Forums/en-US/home?forum=rmscloud)

-   [フォーラム:ユーザー向け RMS (アプリケーション)](https://social.technet.microsoft.com/Forums/en-US/home?forum=rmsapps)

-   [マイクロソフト ヘルプとサポート](http://go.microsoft.com/fwlink/?LinkId=243064)

また、[Microsoft Rights Management サービス ポータル](http://www.microsoft.com/rms)で、[!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] の他のサポート リソースを参照してください。

## 参照
[Azure Rights Management の概要](../Topic/Getting_Started_with_Azure_Rights_Management.md)


---
title: ドキュメントでのリンクの使用方法
description: この記事では、docs.microsoft.com 内でのコンテンツへのリンクの作成に関するガイドを提供します。
author: gewarren
ms.author: gewarren
ms.date: 10/31/2018
ms.openlocfilehash: e56bc0fe3a5428af2a79641a8959b4da21270d53
ms.sourcegitcommit: 44eb4f5ee65c1848d7f36fca107b296eb7687397
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2018
ms.locfileid: "51609432"
---
# <a name="using-links-in-documentation"></a>ドキュメントでリンクを使用する
この記事では、docs.microsoft.com でホストされたページからハイパーリンクを使用する方法について説明します。 いくつかの規則が変更されていますが、リンクは Markdown に簡単に追加できます。 リンクは、同じページ内のコンテンツをポイントするか、他の近くにあるページ内をポイントするか、外部のサイトや URL をポイントすることができます。

docs.microsoft.com サイトは、DocFX Flavored Markdown (DFM) を実装する Open Publishing Services (OPS) をバックエンドで使用します。 DFM は、GitHub Flavored Markdown (GFM) と高い互換性があり、DFM は Markdown 拡張機能を介して機能を追加します。

> [!IMPORTANT]
> ターゲットでサポートされている場合 (このケースが大半) は必ず、すべてのリンクをセキュリティで保護する必要があります (`http` ではなく `https`)。

## <a name="link-text"></a>リンク テキスト

リンク テキストに含める単語はわかりやすくすることをお勧めします。 つまり、通常の英単語にするか、リンク先のページのタイトルにします。

> [!IMPORTANT]
> 「ここをクリック」は使用しないでください。 検索エンジンの最適化としては好ましくなく、リンク先の説明としても的確ではありません。

**正確:**

- `For more information, see the [contributor guide index](https://github.com/Azure/azure-content/blob/master/contributor-guide/contributor-guide-index.md).`

- `For more details, see the [SET TRANSACTION ISOLATION LEVEL](https://msdn.microsoft.com/library/ms173763.aspx) reference.`

**不正確:**

- `For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).`

- `For more information, click [here](https://github.com/Azure/azure-content/blob/master/contributor-guide/contributor-guide-index.md).`

## <a name="links-from-one-article-to-another"></a>1 つの記事から別の記事へのリンク

同じ docset 内で 1 つの Docs 技術情報記事から別の Docs 技術情報記事へのインライン リンクを作成するには、次のリンク構文を使用します。

- ディレクトリの記事を、同じディレクトリの別の記事にリンクする場合

  `[link text](article-name.md)`

- サブディレクトリの記事を、ルート ディレクトリの記事にリンクする場合

  `[link text](../article-name.md)`

- ルート ディレクトリの記事を、サブディレクトリの記事にリンクする場合

  `[link text](./directory/article-name.md)`

- サブディレクトリの記事を、別のサブディレクトリの記事にリンクする場合

  `[link text](../directory/article-name.md)`

- docset 間の記事のリンク (同じリポジトリ内の場合でも):  `[link text](./directory/article-name)`

> [!IMPORTANT]
> 上記の例で `~/` をリンクの一部としているのはありません。 リポジトリのルートにあるパスにリンクするには、`/` から始めます。 GitHub のソース リポジトリを移動するときに `~/` が生成する無効なリンクを含みます。 `/` が正しく解決するパスから始めます。

## <a name="links-to-anchors"></a>アンカーへのリンク

アンカーを作成する必要はありません。 アンカーは、公開時に、すべての H2 見出しについて自動的に生成されます。 唯一行う必要がある処理は、H2 セクションへのリンクを作成することです。

- 同じ記事内の見出しにリンクする場合

  `[link](#the-text-of-the-H2-section-separated-by-hyphens)`
  `[Create cache](#create-cache)`

- 同じサブディレクトリの別の記事のアンカーにリンクする場合

  `[link text](article-name.md#anchor-name)`
  `[Configure your profile](media-services-create-account.md#configure-your-profile)`

- 別のサービスのサブディレクトリのアンカーにリンクする場合

  `[link text](../directory/article-name.md#anchor-name)`
  `[Configure your profile](../directory/media-services-create-account.md#configure-your-profile)`

## <a name="links-from-includes"></a>インクルードからのリンク

インクルード ファイルは別のディレクトリにあるため、より長い相対パスを使用する必要があります。 インクルード ファイルから記事にリンクするには、次のフォーマットを使用します。

   ```markdown
   [link text](../articles/folder/article-name.md)
   ```

## <a name="links-in-selectors"></a>セレクターのリンク

セレクターは、ドロップダウン リストとしてドキュメント記事に表示されるナビゲーション コンポーネントです。 閲覧者がドロップダウンの値を選択すると、選択した記事がブラウザーで開きます。 通常、セレクター リストには、関連性の高い記事のリンクが含まれます。たとえば、同じ題目が複数のプログラミング言語で提示されたり、関連性の高い一連の記事が提示されたりします。 

セレクターがインクルードに埋め込まれている場合、次のリンク構造を使用してください。

   ```markdown
   > [AZURE.SELECTOR-LIST (Dropdown1 | Dropdown2 )]
   - [(Text1 | Example1 )](../articles/folder/article-name1.md)
   - [(Text1 | Example2 )](../articles/folder/article-name2.md)
   - [(Text2 | Example3 )](../articles/folder/article-name3.md)
   - [(Text2 | Example4 )](../articles/folder/article-name4.md) -->
   ```

## <a name="reference-style-links"></a>参照形式のリンク

参照形式のリンクを使用することで、ソース コンテンツをさらに読みやすくすることができます。 参照形式のリンクを使用すると、インライン リンク構文を、簡素化された構文で置き換えることができます。この構文によって、長い URL を記事の最後に移動することができます。 [Daring Fireball](https://daringfireball.net/projects/markdown/) の例を次に示します。

インライン テキスト:

   ```markdown
   I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].
   ```

記事の最後のリンク参照:

   ```markdown
   <!--Reference links in article-->
   [1]: http://google.com/
   [2]: http://search.yahoo.com/
   [3]: http://search.msn.com/
   ```
   
コロンの後、リンクの前に必ずスペースを入れます。 他の技術情報記事にリンクする際に、スペースを入れ忘れてしまった場合、リンクが破損した状態で記事が公開されます。

## <a name="links-to-pages-that-are-not-part-of-the-technical-documentation-set"></a>技術ドキュメント セットではないページへのリンク

別の Microsoft 資産のページ (価格のページ、SLA のページ、その他ドキュメントの記事ではないもの) にリンクする場合は、絶対 URL を使用しますが、ロケールは省略します。 ここでの目的は、リンクが GitHub と次に示すサイトで作動することです。

   ```markdown
   [link text](https://azure.microsoft.com/pricing/details/virtual-machines/)
   ```
   
## <a name="links-to-third-party-sites"></a>サード パーティのサイトへのリンク

最高のユーザー体験は、別サイトへのユーザーの誘導を最小限に抑えます。 そのため、サード パーティのサイトにリンクする必要がある場合は、次の情報に基づいて行ってください。

- **アカウンタビリティ**: 共有する情報がサード パーティの情報である場合に、サード パーティのコンテンツにリンクする。 たとえば、Microsoft のサイトで Android Developer Tools の使用方法の説明はしません。これは、Google が説明するべきことです。 必要であれば、Azure *で* Android 開発者用ツールを使用する方法を説明することはできますが、Google のツールの使用方法は、Google が説明することです。
- **PM サインオフ**: サードパーティ コンテンツの Microsoft サインオフを要求する。 サード パーティのコンテンツにリンクすることは、Microsoft がそのコンテンツを信頼していること、またユーザーがその指示に従った場合の Microsoft の責任を意味することになります
- **情報の鮮度のレビュー**: サード パーティの情報がまだ最新で、間違いがなく、関連していること、そしてリンクが変更していないことを確認する。
- **オフサイト**: 別のサイトに移動していることをユーザーが認識できるようにする。 それが明確でない状況の場合は、適切なフレーズを追加します。 たとえば、"必要条件に Android Developer Tools が含まれます。このツールは Android Studio サイトでダウンロードできます" などです。
- **次のステップ:** 「次のステップ」セクションに、MVP のブログなどへのリンクを追加しても構いません。 この場合も、サイトを離れることをユーザーが必ず認識できるようにしてください
- **合法**: Microsoft は、各 ms.com ページにある「**利用条件**」のフッターの **「サード パーティのサイト」へのリンク**で、合法的に保護されています

## <a name="links-to-msdn-or-technet"></a>MSDN または TechNet へのリンク

MSDN または TechNet へのリンクが必要な場合は、そのトピックへのフル リンクを使用し、そのリンクから "en-us" の言語ロケールを削除します。

## <a name="links-to-azure-powershell-reference-content"></a>Azure PowerShell 関連コンテンツへのリンク

Azure PowerShell 関連のコンテンツは、2016 年 11 月以来、数回の変更を重ねています。 docs.microsoft.com の他の記事からこのコンテンツにリンクする場合は、次のガイドラインを使用してください。

URL の構造:

* コマンドレットの場合:
  - `/powershell/module/<module-name>/<cmdlet-name>[?view=<moniker-name>]`
* 概念についてのトピックの場合:
  - `/powershell/azure/<topic-file-name>[?view=<moniker-name>]`
  - `/powershell/azure/<service-name>/<topic-file-name>[?view=<moniker-name>]`

`<moniker-name>` 部分は任意です。 省略した場合は、コンテンツの最新バージョンに移動します。 `<service-name>` 部分は次のベース URL に示す例のいずれかです。

- Azure PowerShell (AzureRM) のコンテンツ: [https://docs.microsoft.com/powershell/azure/](https://docs.microsoft.com/powershell/azure/)
- Azure PowerShell (ASM) のコンテンツ: [https://docs.microsoft.com/powershell/azure/_servicemanagement_](https://docs.microsoft.com/powershell/azure/servicemanagement)
- Azure Active Directory (AzureAD) PowerShell のコンテンツ: [https://docs.microsoft.com/powershell/azure/_active-directory_](https://docs.microsoft.com/powershell/azure/active-directory)
- Azure Service Fabric PowerShell: [https://docs.microsoft.com/powershell/azure/_service-fabric_](https://docs.microsoft.com/powershell/azure/service-fabric)
- Azure Information Protection PowerShell: [https://docs.microsoft.com/powershell/azure/_aip_](https://docs.microsoft.com/powershell/azure/aip)
- Azure Elastic DB Jobs PowerShell: [https://docs.microsoft.com/powershell/azure/_elasticdbjobs_](https://docs.microsoft.com/powershell/azure/elasticdbjobs)

これらの URL を使用すると、コンテンツの最新バージョンにリダイレクトされます。 この方法を使うと、バージョン モニカーを指定する必要はありません。 また、バージョンが変わったときに更新する必要がある概念的コンテンツへのリンクも保持しません。

正確なリンクを作成するには、リンクするページを自分のブラウザーで検索して、その URL をコピーします。
次に、`https://docs.microsoft.com` とロケール情報を削除します。

目次からリンクするときは、フル URL からロケール情報を削除したものを使用する必要があります。

Markdown の例

```markdown
[Get-AzureRmResourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup)
[Get-AzureRmResourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup?view=azurermps-4.1.0)
[New-AzureVM](/powershell/module/azure/new-azurevm?view=azuresmps-4.0.0)
[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)
[Install Azure PowerShell for Service Management](/powershell/azure/servicemanagement/install-azurerm-ps)
[Install Azure PowerShell](/powershell/azure/install-azurerm-ps)
```

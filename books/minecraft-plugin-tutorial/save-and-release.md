---
title: 【重要】作ったプラグインが消えないように保存する方法
---

このチュートリアルで使っている開発環境「GitHub Codespaces」は、実はとても重要な注意点があります。
それは、**30日以上アクセスしないと、環境がまるごと自動で削除されてしまう**ことです。

せっかく作ったプラグインのコードが消えてしまったら、とても悲しいですよね。

この章は**とても大切な応用編**です。
Codespace が消えても大丈夫なように、**作ったプラグインをGitHubに保存し、安全に永久保存する方法**を学びましょう。

GitHubに保存しておけば、コードが消える心配がなくなるだけでなく、いつでも「昨日の状態に戻す」といったことも可能になります。

この作業は、**次に新しいプラグインを作る時**からぜひ実践してみてください。

---

ここからは、**新しいプラグイン開発を始める場合の手順**を説明します。

:::message
**前の章で作ったプラグインを保存したい場合**
後述の手順でテンプレートからプロジェクトを作成した後、前の章で作った Codespace から下記ファイルをコピペしてください。
- `src` フォルダ
- `spec` フォルダ
- `pom.xml` ファイル

※ 旧Codespaceでフォルダを右クリックして「ダウンロード」し、新しいCodespaceにドラッグ&ドロップでアップロードすると簡単です。
:::

## 🎯 この章でやること
- テンプレートから自分のリポジトリを作成
- 変更をGitHubに保存（コミット＆プッシュ）
- 他の人が使えるように公開（リリース）

## 1. テンプレートからリポジトリを作る
今回使用したテンプレートリポジトリは筆者のアカウントに紐づいており、そのままでは保存することができません。
テンプレートをコピーして新規にリポジトリを作ることで、変更を保存することができるようになります。

1. 以下のテンプレートを開きます。

https://github.com/Kamesuta/minecraft-plugin-maker

2. 「Use this template」から「Create a new repository」を押します。
	![](/images/minecraft-plugin-tutorial/save-and-release/github-template-use-this-template.png)

3. プラグイン名を入れて「Create repository」を押します。
	![](/images/minecraft-plugin-tutorial/save-and-release/github-template-create-repo.png)

4. コピーが完了すると、リポジトリページが開きます。
	![](/images/minecraft-plugin-tutorial/save-and-release/github-template-repo-created.png)
	*(Kamesuta/ChatGrass リポジトリができました)*
5. テンプレート作成後は、2～4章で行った手順と同様にCodespaceのセットアップを行いましょう。
6. 5章のプラグイン制作は、コードの変更をGitHubに保存しながら進めていきますので、次のステップに進んでください。

## 2. 変更をGitHubに保存する
GitHubでは「コミット」→「プッシュ」という操作をすることで、その時点のソースコードをGitHubに保存する事ができます。
:::message
**Tips**: コミット、プッシュとは？
- コミット = ソースコードの変更を「変更履歴」という形で手元(Codespace内)に保存すること、または保存された変更履歴のこと。
- プッシュ = 手元に保存されたコミットをGitHubサーバー上(Codespace外)にアップロードすること
- コミットをこまめにしておけば、あとでその時点まで戻すことができます。
:::

1. `/setup` コマンドを叩いて仕様書が完成すると、左の「ソース管理」アイコンに数字がつくのでクリックして開きます。
	![](/images/minecraft-plugin-tutorial/save-and-release/vscode-source-control-panel.png)
2. メッセージ欄になにをしたか簡単に記載し、緑色の「コミット」ボタンを押します。
	(メッセージは後で履歴を振り返るときに役立ちます)
	![](/images/minecraft-plugin-tutorial/save-and-release/vscode-commit-message.png)
	ダイアログが出たら「常時」を選びましょう。
	![](/images/minecraft-plugin-tutorial/save-and-release/vscode-commit-always-dialog.png)
	*「常時」を選んでおくことで次回から聞かれなくなります。*
4. 「変更を同期 1」という表示に変わるので、クリックすることで**プッシュ**されます。
	![](/images/minecraft-plugin-tutorial/save-and-release/vscode-sync-changes-button.png)
	ダイアログが出たら「OK、今後は表示しない」を選んでおきましょう
	![](/images/minecraft-plugin-tutorial/save-and-release/vscode-sync-confirm-dialog.png)
5. これで保存は完了です！Codespaceを削除してもソースコードは失われません。
6. ステップ1で開いた「リポジトリページ」を開き、仕様書がコミットされているか確認してみましょう。
	![](/images/minecraft-plugin-tutorial/save-and-release/github-repository-commits.png)

変更が失われないようにこまめにコミット＆プッシュする癖をつけておきましょう。
:::message
**Tips**: 巻き戻したくなった場合
履歴を確認したり巻き戻したくなった場合はGit Graphを使うことで操作できます。
![](/images/minecraft-plugin-tutorial/save-and-release/vscode-git-graph.png)
操作方法など気になった方はグーグル検索してみてください。
https://www.google.com/search?q=git+graph+%E8%A7%A3%E8%AA%AC
:::

## 3. 他の人が使えるように公開する（リリース）
GitHubに保存しただけでは、他の人がプラグイン（jarファイル）を簡単にダウンロードすることはできません。

GitHubの「リリース」という機能を使うと、特定のバージョンのプラグインを配布用に公開できます。

1. プラグインをダウンロードする
	 Codespace 内の `target/～～～～-1.0-SNAPSHOT.jar` を右クリックして「ダウンロード...」
	![](/images/minecraft-plugin-tutorial/save-and-release/vscode-download-jar.png)
2. ステップ1で開いた「リポジトリページ」を開く
3. 「Create a new release」
	![](/images/minecraft-plugin-tutorial/save-and-release/github-create-release.png)
	:::message
	2回目以降は「Releases」→「Draft a new release」で開く。
	![](/images/minecraft-plugin-tutorial/save-and-release/github-draft-new-release.png)
	:::
4. タグを作成（例: `v1.0`）し、ダウンロードしたjarファイルをドラッグ&ドロップで添付
	![](/images/minecraft-plugin-tutorial/save-and-release/github-release-upload-assets.png)
5. 「Publish release」を押して公開
6. 公開できたらURLを友だちに送ったり、SNSでシェアしよう
	![](/images/minecraft-plugin-tutorial/save-and-release/github-release-published.png)
:::message
ステップ1でPrivateリポジトリに設定した方は、ここでリリースしても友だちが見ることができません。
jarファイルを直接Discordなどで送信して共有しましょう。
:::

## おまけ: Codespace を削除する

Codespaceは存在するだけで「月間ストレージ量」を消費していきます。
そのため、不要になったCodespaceは削除する必要があります。
### Codespaceの削除方法
:::message
プッシュしていないソースコードは失われるので要注意
消したくない変更はGitHubにプッシュしておきましょう。
:::

1. 下記のCodespace管理ページを開く

https://github.com/codespaces/

2. 消したい Codespace の右側にある「・・・」からDeleteを選びましょう。
	![](/images/minecraft-plugin-tutorial/save-and-release/github-codespaces-menu.png)
3. 本当に消していいか聞かれるので「Delete」を選択
	![](/images/minecraft-plugin-tutorial/save-and-release/github-codespaces-delete-confirm.png)

:::message
なお、「Stop codespace」 を押すことでCodespaceを停止できます。
停止しておくことで月60時間の利用時間を節約できます。
通常、30分間放置することで自動停止されますが、使い終わったらこまめに停止することをおすすめします。

![](/images/minecraft-plugin-tutorial/save-and-release/github-codespaces-stop-button.png)

ちなみに、Codespace内からも停止できます。
![](/images/minecraft-plugin-tutorial/save-and-release/vscode-stop-codespace.png)
:::

## おわりに
ここまで読んでくださり、ありがとうございました。

このチュートリアルを通じて、あなたが自分のアイデアを形にするってこんなに楽しいんだ！と感じていただけたなら幸いです。
ぜひ、あなたの作ったプラグインを友だちに使ってもらったり、SNSでシェアしたりしてみてください。

また、今回のチュートリアルで使った Gemini CLI はまだまだ発展途上の技術です。
今後も進化していくと思いますので、ぜひ注目してみてください。


---
title: 作ったプラグインを安全に保存して公開する方法
---

GitHub Codespaces はとても便利ですが、**30 日間アクセスしないと Codespace がまるごと自動削除**されてしまいます。
せっかく作ったプラグインのソースコードが消えてしまったら、とても悲しいですよね。
Codespace が消えてもソースコードが残るように、**作ったプラグインをGitHubに保存し、安全に永久保存する方法**を学びます。

GitHubに保存しておけば、コードが消えないだけでなく、いつでも「昨日の状態に戻す」といったことも可能になります。

---

ここからは**新しくプラグイン開発を始める場合の手順**を説明します。

:::message
**前の章で作ったプラグインを残したい場合**
後述の手順にて、テンプレートから新しいプロジェクトを作ったあと、以前の Codespace から以下のファイル・フォルダをコピーしてください。
- `src`
- `spec`
- `pom.xml`

旧 Codespace で右クリック→「ダウンロード」、新しい Codespace にドラッグ＆ドロップでアップロードすると簡単です。
:::

## 🎯 この章でやること
- テンプレートから自分専用リポジトリを作る
- 変更をコミット＆プッシュして GitHub に保存する
- jar ファイルをリリースして配布できるようにする

## 1. テンプレートから自分のリポジトリを作成する
筆者のテンプレートはそのままだと保存できないので、自分のアカウントにコピーしましょう。

1. テンプレートを開きます。

https://github.com/Kamesuta/minecraft-plugin-maker
2. 「Use this template」→「Create a new repository」を選択します。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-template-use-this-template.png)
3. 好きなリポジトリ名を入れて「Create repository」を押します。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-template-create-repo.png)
4. テンプレートからリポジトリが作成されると、「リポジトリページ」が開きます。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-template-repo-created.png)
   *例: `Kamesuta/ChatGrass` リポジトリが完成しました*
5. この自分のリポジトリのページから、第 2〜4 章で行った手順と同じように Codespace をセットアップしましょう。
6. 第 5 章以降の開発は、コードの変更をこまめに GitHub に保存しながら進めます。

## 2. 変更を GitHub に保存する（コミット＆プッシュ）
GitHub では「コミット」で履歴を作り、「プッシュ」でサーバーに送ります。これを繰り返すことで安全にコードを残せます。

:::message
**Tips｜用語の整理**
- コミット: 変更内容を手元（Codespace 内）に履歴として記録する操作・履歴のこと。
- プッシュ: 手元のコミットを GitHub 上（Codespace の外）へアップロードする操作。
- こまめにコミットしておくと、後からその時点へ戻せます。
:::

1. `/setup` コマンドで仕様書が生成されると、左側の「ソース管理」アイコンに数字が表示されます。クリックして開きます。
   ![](/images/minecraft-plugin-tutorial/save-and-release/vscode-source-control-panel.png)
2. メッセージ欄に簡単な内容を書いて、緑色の「コミット」ボタンを押します。
   ![](/images/minecraft-plugin-tutorial/save-and-release/vscode-commit-message.png)
   初回はダイアログが出るので「常時」を選んでおくと次回から聞かれません。
   ![](/images/minecraft-plugin-tutorial/save-and-release/vscode-commit-always-dialog.png)
3. ボタン表示が「変更を同期 1」に変わります。クリックすると GitHub へ**プッシュ**されます。
   ![](/images/minecraft-plugin-tutorial/save-and-release/vscode-sync-changes-button.png)
   ダイアログが出たら「OK、今後は表示しない」を選んでおくとスムーズです。
   ![](/images/minecraft-plugin-tutorial/save-and-release/vscode-sync-confirm-dialog.png)
4. これで保存完了です。Codespace を削除しても GitHub 上にソースコードが残ります。
5. Step 1 で開いたリポジトリページを確認し、コミットが反映されているか見てみましょう。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-repository-commits.png)

**ポイント:** 変更が失われないよう、作業の節目でコミット＆プッシュする習慣をつけましょう。

:::message
**Tips｜履歴を戻したくなったら**
`Git Graph` 拡張機能を使うと履歴の確認や巻き戻しが直感的に行えます。
![](/images/minecraft-plugin-tutorial/save-and-release/vscode-git-graph.png)
詳しい使い方は「Git Graph 使い方」などで検索してみてください。
https://www.google.com/search?q=git+graph+%E4%BD%BF%E3%81%84%E6%96%B9
:::

## 3. 他の人が使えるようにリリースする
GitHub に保存しただけでは、他の人が jar ファイルをすぐにダウンロードできません。リリース機能を使って配布できる形にしておきましょう。

1. Codespace 内の `target/〜〜〜〜-1.0-SNAPSHOT.jar` を右クリックし、「ダウンロード...」でローカルに保存します。
   ![](/images/minecraft-plugin-tutorial/save-and-release/vscode-download-jar.png)
2. Step 1 で開いた自分のリポジトリページにアクセスします。
3. 「Create a new release」をクリックします。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-create-release.png)
   :::message
   2 回目以降は「Releases」→「Draft a new release」から作成できます。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-draft-new-release.png)
   :::
4. タグ（例: `v1.0`）を作り、ダウンロードした jar ファイルをドラッグ＆ドロップで添付します。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-release-upload-assets.png)
5. 「Publish release」を押せば公開完了です。
6. 公開した URL を友だちに送ったり、SNS でシェアしましょう。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-release-published.png)

:::message
リポジトリを Private にしている場合は、リリースしても他の人からは見えません。
そのときは jar ファイルを Discord などで直接共有しましょう。
:::

## おまけ: 不要になった Codespace を削除する
Codespace は存在しているだけでストレージ容量を消費します。使い終わったら削除または停止しておきましょう。

:::message
削除すると、プッシュしていない変更は失われます。
消したくない作業は必ず GitHub にプッシュしておいてください。
:::

### Codespace を削除する手順
1. 管理ページを開きます。
   https://github.com/codespaces/
2. 削除したい Codespace の右側にある「…」メニューから Delete を選びます。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-codespaces-menu.png)
3. 確認ダイアログで「Delete」を押すと削除完了です。
   ![](/images/minecraft-plugin-tutorial/save-and-release/github-codespaces-delete-confirm.png)

:::message
「Stop codespace」を選ぶと一時停止できます。
月 60 時間の無料枠を節約したいときに便利です。
30 分放置すると自動停止しますが、使い終わったら自分で停止しておくと安心です。

![](/images/minecraft-plugin-tutorial/save-and-release/github-codespaces-stop-button.png)

Codespace 内からも停止できます。
![](/images/minecraft-plugin-tutorial/save-and-release/vscode-stop-codespace.png)
:::

## おわりに
最後まで読んでいただきありがとうございました。

このチュートリアルを通して、アイデアを形にする楽しさを味わってもらえたなら嬉しいです。
作ったプラグインは友だちに配ったり、SNS で紹介したり、ぜひ活用してみてください。

今回使った Gemini CLI も日々進化しています。
これからのアップデートにも注目してみましょう。

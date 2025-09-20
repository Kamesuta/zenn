---
title: GitHubのアカウント作成～プロジェクトを開くまで
---

この章では、開発の準備として「GitHub アカウントの作成」と「Codespace の起動」を行います。
この準備が完了すれば、あとの作業はすべてブラウザ上で行えます。

## 🎯 この章でやること

- GitHub アカウント作成/ログイン
- Codespace を起動して開発環境を整える

## 1. GitHub アカウントを作る

- すでに持っていれば、ログインだけで OK です。
- 初めての方は次の記事を参考に作成してください。

https://qiita.com/hanamr8ngineer/items/b62dc3b89d789250adbb

## 2. Codespace を開く

今回は、クラウド上の開発 PC「GitHub Codespaces」を使って、ブラウザだけで開発します。

まずは、下記のテンプレートリポジトリを開きましょう。
https://github.com/Kamesuta/minecraft-plugin-maker

1. リポジトリページで緑の「Code」ボタン → 「Codespaces」タブ → 「+」で新規作成  
   ![](/images/minecraft-plugin-tutorial/github-to-codespaces/codespace-create.png)
2. ブラウザ上に VS Code が開き、セットアップが自動で進みます。  
   ![](/images/minecraft-plugin-tutorial/github-to-codespaces/codespace-welcome.png)  
   ![](/images/minecraft-plugin-tutorial/github-to-codespaces/codespace-build-image.png)  
   ![](/images/minecraft-plugin-tutorial/github-to-codespaces/codespace-setup-wait.png)  
   セットアップ中、右下に通知が出ますが、関係ないので ☓ で閉じて OK です。
   ![](/images/minecraft-plugin-tutorial/github-to-codespaces/notification-close.png)
3. 数分待つと、画面下部のターミナルに「★ セットアップスクリプトが完了しました。」のような表示が出れば準備完了です。  
   ![](/images/minecraft-plugin-tutorial/github-to-codespaces/setup-script-complete.png)

:::message
通信が遅い環境では 10 分前後かかることがあります。待っている間に次章をざっと眺めておきましょう。
:::

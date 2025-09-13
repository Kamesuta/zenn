---
title: Gemini CLIのセットアップ
---

Google のプログラミング AI「Gemini CLI」を Codespace で使えるように設定します。
この手順では Google アカウントへのログインが必要ですので、あらかじめご用意ください。

:::message
Gemini CLI を使うためには 18 歳以上に設定された Google アカウントが必要です。
保護者のアカウントを借りるなどしてご用意ください。
:::

## 🎯 できること

- Gemini CLI にログインし、Codespace で使えるようにする

## 1. Gemini CLI を起動する

1. `F1`キーを押して、**コマンドパレット**を開きます。
2. 検索窓に「gemini cli」と入力し、「**Gemini CLI: Run**」を選択してください。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/command-palette-gemini-cli.png)
3. 画面下部にターミナル（コマンドを入力する黒い画面）が開きます。
   見やすいように右側へ移動させておくと、後の作業がスムーズです。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/terminal-move.gif)

## 2. ブラウザで認証してコードをコピーする

1. ターミナルに表示された長い URL を `Ctrl`キーを押しながらクリックします。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-cli-auth-url.png)
2. 「リンクを開きますか？」という確認が表示されたら「開く」をクリックします。
   ブラウザで Google のログインページが開きます。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/terminal-open-web-link.png)
3. Google アカウントでログインします。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/google-login.png)
4. 「Copy」ボタンを押して、表示された認証コードをコピーします。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/google-auth-code.png)

## 3. ターミナルに貼り付けて完了

1. Codespace に戻り、Gemini CLI を起動したターミナル上で右クリックして認証コードを貼り付けます。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/terminal-paste-code.png)
   :::message
   ブラウザによっては、クリップボードへのアクセス許可を求められる場合があります。その際は「許可」をクリックしてください。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/clipboard-permission.png)
   :::
2. ログインに成功すると、追加の質問が表示されることがあります。
   「Do you want to connect GitHub Codespaces to Gemini CLI?」と聞かれたら、そのまま `Enter`キーを押して進んでください。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-cli-login-success.png)
3. 以下の画面が表示されれば、セットアップは完了です。
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-cli-ready.png)

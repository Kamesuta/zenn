---
title: マイクラサーバー起動～ポート開放
---

この章では、Codespace 上で Minecraft サーバーを起動します。
そして、起動したサーバーに自分や友達の PC から接続できるよう、ポート開放という作業を行います。
OP 権限の付与方法や、接続できない場合の対処法についても説明します。

## 🎯 この章でやること

- F5 で Minecraft サーバー起動
- Secure Share Net で 25565 番を公開
- マイクラから接続

## 1. サーバーを起動する

1. VS Code で `F5` を押します。
2. ターミナルにログが流れ、Minecraft サーバーが起動します。
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/debug-start.gif)
   :::message
   右に出る通知は無視して OK です（バツで閉じる）。
   :::
3. `Done (XX.XXXs)! For help, type "help"` と表示されれば起動完了です。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/server-started-done.png)

   :::message
   **起動に失敗したら？**

   ターミナル右上のゴミ箱を押して停止し、もう一度 F5 押せば直ります。
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/console-retry.png)
   :::

## 2. ポートを開放する

Codespaces はデフォルトでは外部から接続できないので、Secure Share Net という有志のポート開放サービスを使ってポート開放します。

:::details Secure Share Net とは？
有志が開発・運営している、無料で使えるゲーム向けのポート転送サービスです。
https://gsht.io/

詳しい使い方は以下の記事が参考になります。
https://agepote.jp/mcserver/gameserver-hostingtool
:::

1. 画面右の「Open Port」を開きます。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/secure-share-open-port.png)
2. ポート番号に `25565` を入力して「公開する」を押します。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/secure-share-port-form.png)
3. 表示された接続情報（ホスト名や IP）をマイクラのマルチプレイにコピペして接続します。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/copy-ip-to-minecraft.png)

   :::message
   **満員で公開できないときは？**

   - 「公開番号」「公開サーバー」を変えて再試行。
     ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/secure-share-rotate-server.png)
   - それでもダメならページ下部の『時間制限付き招待キー』を発行して上部の招待キー欄に貼り付けるとうまくいくことがあります。
     ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/secure-share-invite-key.png)

   :::

## おまけ: OP を付与する

1. 右の「Start Server」からコンソールを開きます。
2. `op <あなたのプレイヤー名>` を実行します。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/grant-op-console.gif)

## おまけ: GitHub CLI でのポート転送（中級者向け）

「Secure Share Net」が使えない場合は、こちらの方法を試してください。

:::details 少し難しい内容のため、クリックして開きます
自分だけが接続する用途であれば、GitHub の公式 CLI を使って自分の PC にポートを転送できます。

1. 手元の PC で Windows PowerShell を開きます。
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/gh-cli-powershell.png)

2. GitHub CLI をインストール

   ```powershell
   winget install --id GitHub.cli
   ```
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/gh-cli-install.png)

   - 「'msstore' ソースでは、使用する前に次の契約を表示する必要があります。」と聞かれたら `Y` を入力して `Enter` キーを押してください。
   - 「このアプリがデバイスに変更を加えることを許可しますか？」と聞かれたら `はい` をクリックしてください。
      ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/gh-cli-sudo.png)

3. ここで一旦、PowerShell ウィンドウを閉じて、もう一度開きます。

4. GitHub アカウントと連携（Codespace 権限付与）
   (先ほどと同様にコピペしてEnterを押してください。)

   ```powershell
   gh auth login -h github.com -p ssh -s codespace -w --skip-ssh-key
   ```

   コマンドを実行すると、「Press Enter」と表示されるので、`Enter` キーを押します。
   その後、ブラウザが開くので XXXX-XXXX をコピーし GitHub アカウントでログインします。
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/gh-cli-auth.gif)

5. 25565 をローカルに転送

   ```powershell
   gh codespace ports forward 25565:25565
   ```
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/gh-cli-port-forward.gif)

   ポート転送が開始されたら、その PowerShell ウィンドウは閉じずに実行したままにしてください。

:::

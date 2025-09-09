---
title: マイクラサーバー起動～ポート開放
---

ブラウザ上のVS Code（Codespaces）からPaperサーバーを起動し、外部から接続できるようにポートを開放します。OP付与や、繋がらない場合の別解（GitHub CLI）もおまけで紹介します。  

できること  
- F5でPaperサーバー起動  
- Secure Share Netで25565番を公開  
- マイクラから接続できる  

## 1. サーバーを起動する  
1. VS Codeで `F5` を押します。  
2. ターミナルにログが流れ、Paperサーバーが起動します。  
3. `Done (XX.XXXs)! For help, type "help"` と表示されれば起動完了です。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/server-started-done.png)  

Tips: 右に出る通知は無視してOKです（バツで閉じる）。  

起動に失敗したら？  
- ターミナル右上のゴミ箱を押して停止し、もう一度F5してください。  
  ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/console-retry.png)  

## 2. ポートを開放する（Secure Share Net）  
Codespacesはデフォルトでは外部から接続できません。公開用トンネルとして Secure Share Net を使います。  

1. 画面右の「Open Port」を開きます。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/secure-share-open-port.png)  
2. ポート番号に `25565` を入力して「公開する」を押します。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/secure-share-port-form.png)  
3. 表示された接続情報（ホスト名やIP）をマイクラのマルチプレイにコピペして接続します。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/copy-ip-to-minecraft.png)  

満員で公開できないときは？  
- 「公開番号」「公開サーバー」を変えて再試行。  
- それでもダメならページ下部の『時間制限付き招待キー』を発行して上部の招待キー欄に貼り付けるとうまくいくことがあります。  

## おまけ: OPを付与する  
1. 右の「Start Server」からコンソールを開きます。  
2. `/op <あなたのプレイヤー名>` を実行します。  
   ![](/images/minecraft-plugin-tutorial/start-server-and-open-port/grant-op-console.png)  

## おまけ: GitHub CLIでのポート転送（自分用）  
Secure Share Netがどうしても使えない場合、自分だけで繋ぐ用途ならGitHub CLIでローカル25565に転送できます（Windows PowerShell例）。  

1) GitHub CLIをインストール  
```powershell
winget install --id GitHub.cli
```

2) GitHubアカウントと連携（Codespace権限付与）  
```powershell
gh auth login -h github.com -p https -s codespace -w
gh auth refresh -h github.com -s codespace
```

3) 25565をローカルに転送  
```powershell
gh codespace ports forward 25565:25565
```
ポート転送が開始されたら、そのPowerShellウィンドウは閉じずに実行したままにしてください。  

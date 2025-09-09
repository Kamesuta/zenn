---
title: Geminiセットアップ
---

GoogleのAIアシスタント「Gemini」をVS Codeから使えるようにします。無料で使えますが、年齢制限があります（18歳以上）。  

できること  
- VS CodeからGeminiにログイン  
- 認証コードをターミナルに貼り付け  

注意  
- 18歳未満のアカウントでは使えません。保護者のアカウントを借りてログインしてください。  

## 1. 拡張機能からサインイン  
1. 右下のダイヤ型アイコン「♦」をクリックします。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-signin-button.png)  
2. 「Sign in」を押します。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-signin.png)  

## 2. ブラウザで認証し、コードをコピー  
1. ターミナルにURLが出るのでCtrl+クリックで開きます。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-cli-auth-url.png)  
2. Googleアカウントでログインします。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/google-login.png)  
3. 表示された認証コードを「Copy」ボタンでコピーします。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-auth-code.png)  

## 3. ターミナルへ貼り付けて完了  
1. VS Code のターミナル上で右クリックすると貼り付けられます。許可を求められたら「許可」してください。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/terminal-paste-code.png)  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/clipboard-permission.png)  
2. ログインが完了すると、成功メッセージが表示されます。  
   ![](/images/minecraft-plugin-tutorial/setup-gemini/gemini-login-success.png)  

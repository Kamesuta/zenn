---
title: Minecraftバージョンの変え方
---

使っているテンプレートに合わせて、Paper（またはAPI）のバージョン定義を変更し、再ビルドします。テンプレートごとに設定場所の名前が少し違う場合があるので、READMEや`build.gradle*`を一緒に確認してください。  

できること  
- 依存バージョンを更新  
- 再ビルドして起動確認  

一般的な手順（Gradleベースの例）  
1. ルートの `build.gradle` または `build.gradle.kts` を開く  
2. `dependencies { ... }` にある Paper API の座標や、`gradle.properties` にある `minecraftVersion` などの値を変更  
   - 例（ktsの一例）: `implementation("io.papermc.paper:paper-api:<新しいPaperバージョン>+")`  
   - プロパティ管理の場合: `minecraftVersion=1.21.1` のような形  
3. 変更を保存すると依存解決が走ります（完了まで待つ）  
4. `F5` でサーバーを起動し、ログに表示されるMinecraft/Paperのバージョンを確認  

注意  
- メジャー/マイナーアップデートではAPIの非互換が出ることがあります。ビルドエラーや警告が出たら、エラーメッセージをGeminiに貼り付けて修正案をもらうのが安全です。  
- 既存のプラグインや設定と合わない場合は、対象箇所を条件分岐したり設定で切り替えられるようにするとスムーズです。  

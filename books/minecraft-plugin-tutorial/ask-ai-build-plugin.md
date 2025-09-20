---
title: AIにお願いしてプラグインを作ってもらおう
---

いよいよ、AIに世界にひとつだけのオリジナルプラグインを作ってもらう時間です！
前章で準備した Gemini CLI のターミナルで、チャットのように要望を伝えるだけ。
プログラミングの知識がなくても、AI があなたのアイデアを形にしてくれます。

## 🎯 この章でやること
- 作りたいプラグインの要望を伝える
- AI が作った最初のバージョンをテストする
- 改善点や追加機能を AI に依頼する

## 1. 魔法の呪文「/setup」を唱える
Gemini CLI のターミナルで `/setup` と入力して `Enter` を押します。
これが、プラグイン作りを始めるための最初の合図です。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-setup-command.png)

## 2. 作りたいプラグインを伝える
`/setup` を実行すると、AI が「何のプラグインを作りたいですか？」と聞いてきます。
難しく考えず、あなたが「あったらいいな」と思うアイデアを、チャットのように伝えてみましょう。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-ask-for-plugin.png)
*(今回は「チャット欄でｗｗｗｗって打ったら周りに草が生えてほしい」という要望を伝えました。)*

**お願いの例:**
> チャット欄でｗｗｗｗって打ったら周りに草が生えてほしい

> プレイヤーがジャンプしたときに花火が上がるようにしてほしい

> 溶岩の下が黒焦げになってほしい


## 3. 計画を確認する
AI があなたの要望をもとに「こんな感じですか？」という計画案を提示します。

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-plan-proposal.png)
*(今回は問題なさそうだったので「はい」と答えました。)*

内容がイメージ通りなら、そのまま進みましょう。
考えているものと違う場合は、AI に修正を依頼します。

**お願いの例:**
> 「ｗ」の数に応じた草を生やしてほしい

> 草を生やす場所が土ブロックの場合は、草ブロックに置き換えてほしい

内容を確認して「はい」と答えると、次のステップに進みます。

## 4. 仕様を確認する
計画の確認が終わると、仕様書が開きます。
プレビューボタン（②）を押すと、読みやすく表示されます。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-spec-preview.png)
*(今回は少し違っていたので、以下のように依頼しました。)*

ここでも、イメージと違えば AI に修正を依頼します。


**お願いの例:**
> 「ｗｗｗｗ」で一個の草が生えるんじゃなくて、「ｗ」一個から反応し、個数に応じて反応してほしい。

> 「連続生成を防ぐためのクールダウン機能」は要らない

:::details チャットでのやりとり例 (画像)
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-spec-modification-request.png)
:::

内容を確認して「はい」と答えると、いよいよ開発スタートです。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-development-start-confirmation.png)

## 5. 実装は AI におまかせ
あなたが「はい」と答えると、AI が自動で実装を進めます。
この間は待つだけで OK。難しいプログラミング作業は AI が担当します。

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-implementing.png)

:::message
**うまく動かないときはAIを頼ろう**
途中で困りごとやエラーが出たら、そのまま AI に相談しましょう。
エラーログなどの情報があれば、合わせて伝えると解決が早くなります。
:::

## 6. テストして改善を依頼する
実装が完了すると、サーバーにプラグインが自動導入されます。Minecraft にログインして動作を確認しましょう。

### A. まずはテスト
サーバーに入って、プラグインが正しく動くか試します。

### B. 問題があれば修正を依頼
なるべく具体的に伝えると、修正がスムーズです。

**お願いの例**

> 地面が削れてしまいましたので直したいです。	

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/minecraft-plugin-test.gif)
*(今回は「w」と入力したら地面が削れてしまったので、削れないように修正を依頼します。)*

### C. AI から動作確認を求められたら、結果を伝える
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-ask-for-confirmation.png)

できたことを報告すると、一旦最小限の実装は完了となります！
AIが次に実装する案を提案してくれます。

### D. 次にやりたいことを依頼
やりたいことを依頼しましょう。

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-propose-next-task.gif)
*(今回は「ｗ」を打ったら周りにランダムで草が生えるようにしてほしいと依頼しました。)*

**お願いの例**
> 骨粉を草ブロックに使用したときのように、「ｗ」を打ったら周りにランダムで草が生えるようにしてください

> 2がやりたいです。

### E. そしてまたテスト
この「テストして、次をお願いする」という繰り返しで、あなたのプラグインはどんどん理想に近づいていきます。

:::message
途中で Gemini CLI を終了したり、Codespace を閉じてチャットが失われても、`/setup` を再実行すれば再開できます。
:::

## 7. 完成 🎉
まだ改良の余地はありますが、これでプラグインは完成です。
**ここまで到達できたあなたは立派な Minecraft プラグイン制作者です**✨️。誇りを持ってください！
お疲れさまでした！

次の章では、作ったプラグインが消えないように、ソースコードを保存したり、作られたプラグインファイル (jarファイル) を公開したりする方法を紹介します。

---
title: AIにお願いしてプラグインを作ってもらおう
---

いよいよ、AIに世界に一つだけのオリジナルプラグインを作ってもらう時間です！
前の章で準備した「Gemini CLI」のターミナルに、まるでチャットで話しかけるように「お願い」するだけ。
プログラミングの知識がなくても、あなたのアイデアをAIが形にしてくれます。

## 🎯 この章でやること
- AIに「こんなプラグインが欲しい！」とお願いする
- AIが作った「最初のバージョン」をテストする
- AIに次の機能を追加してもらう

## 1. 魔法の呪文「/setup」を唱えよう
Gemini CLIのターミナルで、`/setup` と入力して `Enter` キーを押してください。
これが、AIにプラグイン作りを始めてもらうための「最初の合図」です。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-setup-command.png)

## 2. AIに「こんなもの作って！」とお願いしてみよう
`/setup` を実行すると、AIが「何のプラグインを作りたいですか？」と聞いてきます。
難しく考えず、あなたが「あったらいいな」と思うプラグインのアイデアを、チャットのように話しかけてみましょう。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-ask-for-plugin.png)

**お願いの例:**
> チャット欄でｗｗｗｗって打ったら周りに草が生えてほしい

> プレイヤーがジャンプしたときに花火が上がるようにしてほしい

> 溶岩の下が黒焦げになってほしい

## 3. 計画を確認する
AIがあなたのアイデアを元に「こんな感じですか？」と計画をまとめてくれます。

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-plan-proposal.png)
今回は問題なさそうなのでそのまま進みます。

考えているものと違った場合、AIにお願いして直してもらいましょう。

**お願いの例:**
> 「ｗ」の数に応じた草を生やしてほしい

> 草を生やす場所が土ブロックの場合は、草ブロックに置き換えてほしい

内容を確認して「はい」と答えれば、次のステップに進みます。
## 4. 仕様を確認
計画の確認が完了すると、仕様書が開かれます。
プレビューボタン (②) を押すと、仕様書が分かりやすく表示されます。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-spec-preview.png)

考えているものと違った場合、AIにお願いして直してもらいましょう。
今回はちょっと考えているものと違ったので、以下のお願いをしてみました。

**お願いの例:**
> 「ｗｗｗｗ」で一個の草が生えるんじゃなくて、「ｗ」一個から反応し、個数に応じて反応してほしい。

> 「連続生成を防ぐためのクールダウン機能」は要らない

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-spec-modification-request.png)

内容を確認して「はい」と答えれば、いよいよ開発スタートです。
![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-development-start-confirmation.png)
## 3. あとはAIにおまかせ！
あなたが「はい」と答えると、AIが魔法のように働き始めます。
この間、あなたはただ待っているだけでOK。難しいプログラミングはすべてAIがやってくれます。

![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-implementing.png)

:::message
**うまく動かないときはAIを頼ろう**
途中で、なにか困ったことやエラーが発生したら、それもAIに聞いてみましょう。
エラーログなどを見つけたら、それもAIに教えてあげてください。
:::
## 4. テストして、次の機能をお願いしよう
実装が完了すると、自動でサーバーにプラグインが導入されるので、Minecraftでサーバーに入って、動作を確認してみましょう。

1.  **テストしよう！**
    サーバーに入って、プラグインがちゃんと動くか試してみましょう。
    ![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/minecraft-plugin-test.gif)
    
2. **なんか微妙だったらAIに修正をお願いしよう！**
	なるべく具体的に伝えてあげると、うまくいくことが多いです。

	**お願い例**
	今回は「w」と入力したら、地面が削れてしまいまったので削れないように修正をお願いしてみます。
	> 地面が削れてしまいましたので直したいです。
	
3. **AIに動作確認を求められた場合は、確認して結果を教えてあげましょう**
	![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-ask-for-confirmation.png)

4.  **次のお願いをしよう**
	できたことを報告すると、次に実装する案を提案してくれるので、やりたいことをお願いしましょう。
	
	![](/images/minecraft-plugin-tutorial/ask-ai-build-plugin/gemini-cli-propose-next-task.gif)

	**お願い例**
	> 骨粉を草ブロックに使用したときのように、「ｗ」を打ったら周りにランダムで草が生えるようにしてください

	> 2がやりたいです。

この「**テストして、次をお願いする**」という繰り返しで、あなたのプラグインはどんどんあなたが考える理想に近づいていきます。

:::message
途中でGemini CLIを終了したり、Codespaceを閉じてしまったりしてチャットが失われてしまった場合、 `/setup` を再び打てば再開できます。
:::
## 5. 完成
まだまだ改良の余地はあるかと思いますが、以上でプラグインは完成です！
ここまでこれたあなたは立派なMinecraftプラグイン制作者です！誇りを持ってください。
お疲れ様です！

次の章では、作ったプラグインが消えないように、ソースコードを保存したり、作られたプラグインファイル(jarファイル)を公開したりする方法を紹介します。
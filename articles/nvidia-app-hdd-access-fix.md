---
title: NVIDIA AppがHDDを100%食いつぶす問題を解決した
emoji: 💾
type: tech
topics:
  - windows
  - nvidia
  - performance
  - geforce
published: true
---
NVIDIA Appが毎日のようにHDDを激しくアクセスする問題に悩まされていた。この問題を解決する方法を紹介する。
## NVIDIA AppがHDDを100%食いつぶす
PC起動直後にHDDがゴリゴリ音を立てる現象が発生している。
リソースモニターを見ると `nvcontainer.exe` がディスクを100%使用していることがわかったので、調べてみた。
![](/images/nvidia-app-hdd-access-fix/2025-05-07_19h27_11.png)
## 原因はゲームのフルスキャン
NVIDIA Appはゲーム一覧を表示するために、ゲームっぽいフォルダを勝手に登録し、フルスキャンをかけるようだ。
私の環境ではCドライブ(SSD)の他にEドライブ(HDD)にソフトを大量に入れていたため、1時間くらいHDDディスクが悲鳴を上げていた。
### スキャンされる場所について
PCにつながっているすべてのドライブがスキャン対象。
`Program Files`の他に、`SteamLibrary`や`Epic Games`フォルダのような"ゲームっぽい"フォルダは自動的にスキャンロケーションとして登録され、毎日バックグラウンドでフルスキャンが走る模様。
![](/images/nvidia-app-hdd-access-fix/2025-05-07_23h31_34.png)
## スキャンする場所の全消しで解決
1. NVIDIA Appを起動 > 設定（⚙️）> 「性能」
2. 「スキャンロケーション」の右にある「表示して修正する」をクリック
	![](/images/nvidia-app-hdd-access-fix/2025-05-07_22h52_08.png)
3. 右側にある削除ボタンを連打してすべて削除する
	![](/images/nvidia-app-hdd-access-fix/2025-05-07_19h25_04.png)
4. 閉じる
5. (必要であれば) リソースモニターから nvcontainer.exe を終了させる (現在のスキャンが強制停止する)
## 注意点
- この設定をすると当然NVIDIA Appのゲーム一覧は更新されなくなる
    - 私の場合はゲーム一覧機能を全く使っていなかったので不便を感じなかった
## 結果
HDDへのアクセスが0%になった。とても静かになって満足。
![](/images/nvidia-app-hdd-access-fix/2025-05-07_19h30_33.png)


---
title: Tailscale でサーバー→作業PCアクセスを完全ブロックする
emoji: 🛡️
type: tech
topics:
  - tailscale
  - security
published: true
---

Tailscaleネットワークにサーバー機と作業PC(ローカルマシン)を追加しているとセキュリティリスクがあるため対策する。

## なぜサーバー→作業PCにアクセスできるのがマズイのか？

私のサーバーは複数人で管理しています。
そのため、別の人が自分のサーバーにSSHで入り、サーバーを踏み台にして自分の作業PCにアクセスできてしまいます。
ローカルで動かしてるテスト用のWebサーバーなどが全部丸見えになってしまいます。

なので、サーバー→作業PCのアクセスはブロックしようと思い立ちました。

## 目指すところ

- ✅ サーバー → サーバー  
- ✅ 作業PC → サーバー  
- ❌ サーバー → 作業PC  
- ✅ 作業PC → 作業PC  

これをシンプルなTailscaleのACLで実現します。

---

## 手順

### 1. Access Controls（ACL）を設定する

Tailscale 管理画面の「Access Controls」タブから、ACL 設定ファイルを編集します。
私の場合以下のようにしました。

```json
{
	"tagOwners": {
		"tag:server": ["autogroup:admin"],
	},
	"acls": [
		// サーバーへのアクセスは全部許可 (ローカルPCへのアクセスは禁止)
		{"action": "accept", "src": ["tag:server"], "dst": ["tag:server:*"]},
		// ローカルPCからのアクセスは全部許可
		{"action": "accept", "src": ["autogroup:member"], "dst": ["*:*"]},
	],
	
	// ... 以下省略 ...
}
```

:::message
💡 Tailscale の ACL は「許可するルール」しか定義できないため、拒否ルールは書けません。  
上記のように「許可したい通信のみ」を明示し、それ以外はデフォルトでブロックされる動作を利用します。
:::

---

### 2. サーバーマシンにタグを付与する

ACL 設定で定義した `tag:server` を、対象のサーバーマシンに付与します。

1. 管理画面の「Machines」一覧からサーバーを選択  
2. 「ACL Tags」に `server` タグを追加
	![サーバーマシンへのタグ付与①](/images/tailscale-restrict-server-to-client/2025-04-22_01h52_39.png)
	![サーバーマシンへのタグ付与②](/images/tailscale-restrict-server-to-client/2025-04-22_01h54_04.png)
	
	:::message
	💡 一度タグを付与すると、Tailscale クライアント側で再認証（再ログイン）が行われるまでタグが反映されません。変更後はクライアントを再起動するか、UI上でログアウト→ログインしてください。
	:::

これでサーバー→作業PCへのアクセスがブロックされました！
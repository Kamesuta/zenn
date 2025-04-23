---
title: Tailscale でサーバー→作業PCアクセスを完全ブロックする
emoji: 🛡️
type: tech
topics:
  - tailscale
  - security
published: true
---

Tailscaleネットワークにサーバー機と作業PC（ローカルマシン）を追加すると、サーバーを踏み台に作業PCに侵入されるリスクがある。
そこでアクセス制限を設定する。

## なぜサーバー→作業PCアクセスが危険なのか

前提として、複数人で管理しているサーバーにTailscaleをインストールして、作業PC→サーバーへ接続することにした。

その場合、特に何もしないと、逆のサーバー→作業PCへのアクセスも可能になってしまう。
すると、サーバーにSSH接続できる他のメンバーから、作業PC上で動かしているテスト用Webサーバーなどが丸見えになってしまう問題が発生した。

そのため、サーバー→作業PCへのアクセスをブロックする設定を行うことにした。

## 目指すアクセスパターン

- ✅ サーバー → サーバー  
- ✅ 作業PC → サーバー  
- ❌ サーバー → 作業PC  
- ✅ 作業PC → 作業PC  

これをシンプルなTailscale ACLで実現する。

---

## 手順

### 1. Access Controls（ACL）を設定する

Tailscale 管理画面の「Access Controls」タブでACL設定ファイルを編集する。

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
💡 TailscaleのACLでは「許可するルール」しか記述できない。
許可したい通信のみを明示し、それ以外はデフォルトでブロックされる動作を利用する。
:::

---

### 2. サーバーマシンにタグを付与する

ACL設定で定義した `tag:server` をサーバー機に割り当てる。

1. 管理画面の「Machines」一覧からサーバーを選択  
2. 「ACL Tags」に `server` タグを追加
	![サーバーマシンへのタグ付与①](/images/tailscale-restrict-server-to-client/2025-04-22_01h52_39.png)
	![サーバーマシンへのタグ付与②](/images/tailscale-restrict-server-to-client/2025-04-22_01h54_04.png)
	
	:::message
	💡 一度タグを付与すると、GUI上からはタグがない状態に戻せなくなる。
	そのため戻すためには、Tailscale クライアント側で再認証が必要。
	:::

これでサーバー→作業PCへのアクセスが完全にブロックされる。

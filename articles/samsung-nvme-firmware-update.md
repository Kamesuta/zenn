---
title: Samsung 980 NVMe 1TB のファームウェアをLinux (Proxmox) からリモートで更新する方法
emoji: 📀
type: tech
topics:
  - proxmox
  - ssd
  - firmwareupdate
  - samsung
  - linux
published: true
---

Samsung公式のファームウェアアップデート方法では、ISOをUSBメモリに焼き、BIOSブートして更新する必要があります。
しかし、サーバーのある実家に行くのは面倒だし、USBの準備も手間ですよね。

そこで今回は**非公式な方法**で、**Proxmox環境からLinux上で直接ファームウェアを更新したので手順**をまとめました。

## 対象環境・背景

* 対象ディスク: `Samsung SSD 980 1TB`
* 現在のファームウェア: `2B4QFXO7`
* 目標バージョン: `3B4QFXO7`
* OS: Proxmox (Debian Linux)

最近、突然認識しなくなってIOエラーが頻発する、という現象が発生していて、もしかしてファームウェアが原因かもしれないのでアップデートしてみることにしました。

## 事前にファームウェアのバージョンを確認する

```bash
sudo apt-get install smartmontools -y
sudo smartctl -a -s on /dev/nvme0n1 | grep "Firmware Version"
```

出力例:
```
Firmware Version:                   2B4QFXO7
```

## アップデートの概要

今回のアップデートでは以下のようなバージョン変更を目指します。

```
2B4QFXO7 → 3B4QFXO7
```

## 実際の更新手順

### 1. VMを停止してNVMeを開放

Proxmox GUIで以下の操作を行う

* LVMに載っている仮想マシンをすべてシャットダウン
* `Datacenter > Storage > nvme(今回のSSD)`を選び、`Edit`から`Enable`のチェックを外す

![](/images/samsung-nvme-firmware-update/2025-05-17_14h44_26.png)

### 2. Samsung公式サイトからISOをダウンロード

以下ページからファームウェアのISOファイルをダウンロードします。

https://semiconductor.samsung.com/consumer-storage/support/tools/

例: `Samsung_SSD_980_3B4QFXO7.iso`

![](/images/samsung-nvme-firmware-update/2025-05-17_13h37_32.png)

```bash
wget https://download.semiconductor.samsung.com/resources/software-resources/Samsung_SSD_980_3B4QFXO7.iso
```

### 3. LinuxからISOをマウント・展開してファームウェア更新

```bash
sudo apt-get -y install gzip unzip wget cpio
mkdir /mnt/iso
sudo mount -o loop ./Samsung_SSD_980_3B4QFXO7.iso /mnt/iso/

mkdir /tmp/fwupdate
cd /tmp/fwupdate
gzip -dc /mnt/iso/initrd | cpio -idv --no-absolute-filenames

cd root/fumagician/
sudo ./fumagician
```

画面に以下のようなインターフェースが表示されるので、アップデートを進めます。

```
______________________________DISK(s) DETECTED______________________________ 
|#|               Drive Model               |    Serial Number    | Firmware |
|1| Samsung SSD 980 1TB                     | S649NX0T177901A     | 2B4QFXO7 |
```

アップデート確認:

```
Do you want to continue the firmware update? [Y/N]: y
```

終了後のメッセージ:

```
Exiting Samsung SSD Firmware Update Utility Ver. 3.1
```

### 4. Proxmoxを再起動

アップデートの反映のため、Proxmoxホストを再起動します。

### 5. ファームウェアの更新確認

```bash
sudo smartctl -a -s on /dev/nvme0n1 | grep "Firmware Version"
```

出力に `Firmware Version: 3B4QFXO7` が表示されていれば成功です。

### 6. NVMeを再EnableしてVMを起動

Proxmox GUIに戻り、`Datacenter > Storage > nvme` で `Enable` を再チェックします。
その後VMを起動し、データ消失などが起きていないことを確認しましょう。

## 最後に

公式ではサポートされていない方法ですが、Linux上からでもSamsung SSDのファームウェア更新できます。
サーバーを物理的に操作しなくてもよいので、リモート管理している環境において非常に有効です。

**ただし、アップデートは自己責任で行ってください～**

### 参考リンク

* [Samsung SSD Firmware Update Utility](https://semiconductor.samsung.com/consumer-storage/support/tools/)
* [Firmware update Samsung SSD in Linux - Intermittent Technology](https://blog.quindorian.org/2021/05/firmware-update-samsung-ssd-in-linux.html/)
* [smartmontools](https://www.smartmontools.org/)


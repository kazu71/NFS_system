# NFSサーバの構築と設定
この記事では、NFSの構築手順を簡単にシンプルに説明しています。
開発履歴として残していますので参考程度に活用ください。
<br>
<br>
## NFSの簡単な仕組み
NFS(network file system)は、他のコンピュータとファイルを共有するためのプロトコルです。今回はLinuxのubuntu serverを使って構築します。
<br>
<br>
## 使用ポート番号
NFSは通常、TCPまたはUDPポート2049を使用します。
ポート開放などの設定は[こちら](https://github.com/kazu71/Ubuntu_System_List/tree/5b8c9541c2ba993d68df45bcc942d6c397fa9683/UFW_System)のリポジトリをご確認ください
<br>
<br>
## NFS システムのインストール

OS の更新します。
```
sudo apt update
```
```
sudo apt upgrade
```
<br>
<br>

更新システムを反映するために再起動を行います。
```
sudo reboot
```
<br>
<br>

システムをインストールします。
```
sudo apt install nfs-kernel-server
```
<br>
<br>

システムを有効にします。
```
sudo systemctl enable nfs-kernel-server
```
<br>
<br>

システムを起動します。
```
sudo systemctl start nfs-kernel-server
```
<br>
<br>

システムが正常に稼働しているかを確認します。
```
sudo systemctl status nfs-kernel-server
```
<br>
<br>

## NFSの設定ファイル
<br>
<br>

NFSの設定は以下のディレクトで行います。
```
/etc/exports
```
<br>
<br>

ファイルを編集するには以下のコマンドを入力します。
今回はnanoで編集をするので以下のコマンドでnanoをインストールします。
```
sudo apt install nano
```
<br>
<br>

上記のnanoのインストールができましたら以下のコマンドファイル編集画面に入ります。
```
sudo nano /etc/exports
```
<br>
<br>
以下のコードを入力します。

```
/home/user1/eclipse_workspace 192.168.0.1(rw,no_root_squash)
```

上記のコードについて簡単に仕組みを説明すると....
- 192.168.0.1は、クライアント側のIPaddress
- /home/user1/eclipse_workspaceは、ファイル共有を行うディレクトリ
- (rw,no_root_squash)の設定や説明は以下をご確認ください。

> roとrwの説明
- ro
<br>
ディレクトリは読み取り専用で共有されるため、クライアントサーバ側のディレクトリに書き込むことはできない。
<br>
<br>

- rw
<br>
クライアントは、サーバ側のディレクトリに読み取り及び書き込みが可能になる。
<br>
<br>

- no_root_squash
<br>
デフォルトでは、クライアント マシン上のユーザー root によって行われたファイル要求は、そのサーバー上のユーザー nobody によって行われたかのように扱われます。このオプションを選択すると、クライアント マシン上の root は、システム上のファイルへのアクセスについて、サーバー上の root と同じレベルのアクセス権限を持ちます。
<br>
<br>






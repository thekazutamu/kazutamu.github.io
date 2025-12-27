+++
draft = false
date = '2025-12-19T23:27:02+09:00'
title = 'HTB: Timelapse'
tags = ['HackTheBox', 'Windows', 'Easy']
+++

## 概要
>  **Machine:** [Timelapse](https://www.hackthebox.com/machines/timelapse)  
>  **OS:** Windows  
>  **Difficulty:** Easy

## ポートスキャン


`nmap`でポートスキャンします。

```bash
sudo nmap -sC -sV $RHOST
```
![img](nmap.png)

`SMBポート(445)`が開いています。

## SMB列挙

`smbclient`で共有フォルダを一覧表示します。

```bash
smbclient -N -L $RHOST
```

> [!NOTE] メモ
> smbclientの使い方は、[こちらの記事](/posts/pentest-tools/smbclient.md)にまとめています。

`Shares`と`SYSVOL`が見つかります。

![img](smbclient.png)

`Shares`にアクセスします。

```bash
smbclient -N //$RHOST/Shares
```

`ls`コマンドで、`Dev`と`HelpDesk`の２つのフォルダが見つかりました。

`mget`コマンドで、`Shares`配下のファイルを一括ダウンロードします。

`exit`コマンドで接続を終了します。


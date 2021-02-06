---
template: blog-post
title: macOS BigSurでapacheがスタートできないときの対処法【ServerName】
slug: /mac_apache_servername_troubleshooting
tags:
  - Apache
date: 2020-05-13 12:46
description: sdasd
featuredImage: /assets/apache.png
---
apache起動しようとして、こんなエラーが出ました。

```shell
AH00558: httpd: Could not reliably determine 
the server's fully qualified domain name, using {アドレス}. 
Set the 'ServerName' directive globally to suppress this message
```

ServerNameが設定されてない？\
ということで、**httpd.conf** を確認してみました。
場所は **/usr/local/etc/httpd/httpd.conf** です。

224行目にありました。これってデフォルトでコメントアウトしてるんですね。

```editorconfig
#
# ServerName gives the name and port that the server uses to identify itself.
# This can often be determined automatically, but we recommend you specify
# it explicitly to prevent problems during startup.
#
# If your host doesn't have a registered DNS name, enter its IP address here.
#
# ServerName www.example.com:8080
```

このコメントアウトを外せばOK。\
DNS名があるならそれを、ないならIPを指定します。

```editorconfig
ServerName localhost:8080
```
これで保存して

```shell
apache start
```
で解決しました。
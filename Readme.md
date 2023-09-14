# Hardening2023 練習環境

## 概要

Wordpress と EC-CUBE が動く vagrant の box を作りました。
インフラには詳しくないので設定周りについてはご容赦ください。

## 動作要件

- virtualbox
- vagrant

## 注意

1. mac でしか動作確認していないので、windows で動くか分かりません
2. `vagrant up`実行するとネットワークレンジエラーが発生するかもしれないです。そのときは`server.vm.network "private_network"`の行をコメントアウトすればとりあえずエラーは解消できます。
3. サーバー起動後、apache が動いていない可能性があります。そのときは`sudo systemctl restart httpd`を実行してください。

## Server1

### 環境

- RockyLinux:8.8
- php:7.4
- mysql:8.0.34
- apache:2.4.37
- wordpress: 6.3.1

linux users(デフォルトはパスワード認証が禁止されてる?ので後述の秘密鍵でsshします):
- root
- vagrant


mysql:
- rootpass: f?XgAWVvt6fS
- dbname: wp
- wpdbuser: wpu
- wpdbuserpass: f?XgAWVvt6fS
- host: localhost

apache:

- DocumentRoot: /var/www/html

wordpress:

- login: /wp-admin
- username: user
- password: TTazwIF2)hQpIZubR4

### サーバー起動

`vagrant up server1`

### サーバーへ接続

`vagrant ssh server1`

### サーバーへ接続(ssh コマンドを使用したい場合)

1. 接続情報取得

`vagrant ssh-config`

以下のような情報が得られます

> Host server1  
>  HostName 127.0.0.1  
>  User vagrant  
>  Port 2223  
>  UserKnownHostsFile /dev/null  
>  StrictHostKeyChecking no  
>  PasswordAuthentication no  
>  IdentityFile /Users/username/.vagrant.d/ insecure_private_key  
>  IdentitiesOnly yes  
>  LogLevel FATAL  
>  PubkeyAcceptedKeyTypes +ssh-rsa  
>  HostKeyAlgorithms +ssh-rsa

2. 接続  
   上記情報を基に書き換えてください  
   `ssh vagrant@127.0.0.1 -p 2222 -i /Users/username/.vagrant.d/insecure_private_key`

### サーバーへ接続(プライベート ip で接続)

`ssh vagrant@172.31.103.10 -i /Users/username/.vagrant.d/insecure_private_key`

### ログイン [http://172.31.103.10/wp-admin/](http://172.31.103.10/wp-admin/)

もしくは [http://127.0.0.1:8888/wp-admin/](http://172.31.103.10/wp-admin/)

## Server2

### 環境

- RockyLinux:8.8
- php:7.4
- postgres: 14.9
- apache:2.4.37
- ec-cube: 4.2.0

postgres:

- rootusername: postgres
- rootpass: psql
- dbname: ecc
- eccdbuser: eccu
- eccdbuserpass: secret
- host: localhost

apache:

- DocumentRoot: /var/www/html
- user: apache
- group: apache

ec-cube:

- login: /ec-cube/admin
- username: admin
- password: password
- AuthMagic: fHLCazYiemiKPCPs

何らかの原因で ec-cube が止まってたら
`symfony server:start --daemon`
で起動

### サーバー起動

`vagrant up server2`

### サーバーへ接続

`vagrant ssh server2`  
前述の他の方法でも接続できます

### ログイン [http://172.31.103.11/ec-cube/admin](http://172.31.103.10/ec-cube/admin)

もしくは [http://127.0.0.1:8889/ec-cube/admin](http://127.0.0.1:8889/ec-cube/admin)


## 備考

- `vagrant up`を実行するとsever1とserver2が同時に立ち上がるのでメモリ容量にご注意ください

|                |                            |     | 
| -------------- | -------------------------- | --- | 
| vagrant up     | 仮想マシンの起動           |     | 
| vagrant halt   | 仮想マシンのシャットダウン |     | 
| vagrant reload | 仮想マシンの再起動         |     | 
| vagrant suspend  | 仮想マシンの一時停止         |     | 
| vagrant resume  | 仮想マシンの一時停止からの復帰         |     | 
| vagrant status  |  仮想マシンのステータスを表示        |     | 
| vagrant destroy -f  | 仮想マシンの削除(virtualboxの一覧から消える)         |     | 
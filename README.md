# README - playbooks

## 概要
RMaaS用環境を構築するPlayBook

## 前提
https://vitallead.backlog.com/alias/file/3894958 の環境構成概要書を確認されたい。
ULTiDCホスティングサービスに特化した固有情報は以下のファイルに集約している。

・group_vars
・host_vars
・hosts

## 使い方
0) init用各種変数群のカスタマイズ

```
init/
├── ansible.cfg
├── group_vars
│   └── init
│       ├── vars.yml     ※ 固有の認証情報(subadmin)
│       └── vault.yml    ※ 固有の認証情報(subadmin)
├── host_vars
│   └── 172.16.10.62.yml ※ 固有のssh ProxyCommandを定義
├── hosts
├── init.yml
└── roles
    └── init
        ├── files
        ├── tasks
        └── vars
```

1) initプレイブックを実行する

```
$ cd init
$ ansible-playbook init.yml --vault-password-file=.ansible_vault_pass
```

2) custom_server用各種変数群のカスタマイズ

```
custom_server/
├── ansible.cfg
├── custom_server.yml
├── group_vars
│   └── custom_server
│       ├── vars.yml     ※ 固有の認証情報(vladmin)
│       └── vault.yml    ※ 固有の認証情報(vladmin)
├── host_vars
│   └── 172.16.10.62.yml ※ 固有のssh ProxyCommandを定義
├── hosts                ※ certsグループをコメントアウト中
└── roles
    ├── certs            ※ Let's Encrytpサーバ証明書を取得・更新する
    │   ├── handlers
    │   ├── tasks
    │   └── vars
    ├── network          ※ ネットワーク関連の諸設定を行う
    │   ├── handlers
    │   ├── tasks
    │   └── vars
    ├── nginx            ※ HTTPサーバ(Nginx)を構築する
    │   ├── files
    │   ├── handlers
    │   ├── tasks
    │   ├── templates
    │   └── vars
    ├── postgresql       ※ DBサーバ(PostgreSQL)を構築する
    │   ├── tasks
    │   └── vars
    ├── postgresql_setup ※ DBサーバのコンフィギャを行う
    │   ├── files
    │   ├── handlers
    │   ├── tasks
    │   └── vars
    ├── puma_auto        ※ Railsアプリケーションサーバ(Puma)を自動起動する
    │   ├── tasks
    │   ├── templates
    │   └── vars
    ├── redis            ※ NoSQL DB(Redis)を構築する
    │   ├── handlers
    │   ├── tasks
    │   └── vars
    ├── ruby             ※ Ruby On Rails環境(rbenv、ruby-build)を構築する
    │   ├── files
    │   ├── tasks
    │   └── vars
    ├── sample_app       ※ サンプルRoRアプリ(helloworld)をデプロイする
    │   ├── files
    │   ├── tasks
    │   └── vars
    └── system           ※ RHEL OS一般の諸設定を行う
        ├── files
        ├── handlers
        ├── tasks
        └── vars
```

3) custom_serverプレイブックを実行する

```
$ cd custom_server
$ ansible-playbook custom_server.yml --vault-password-file=.ansible_vault_pass
```

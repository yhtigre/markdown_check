# README - playbooks

## 概要
バスロケWEBサーバを構築する。

## 準備
Backlog Gitリポジトリからローカル環境へクローンする。
※リビジョン c2f1e7da44 により部分的なチェックアウトは不要となりました

1) 適当なディレクトリ上でBacklog Gitリポジトリをクローンする

```
$ git clone vitallead@vitallead.git.backlog.com:/BUS_LOCA/busloca-infrastructure.git
```

## 使い方
0) 各種変数群のカスタマイズ

tbo_server/group_vars/tbo_server/vars.yml に「lan_address」をカスタマイズする箇所が
あるがIPアドレスが衝突しないように注意する。

```
.
└── playbooks
    ├── init
    │   ├── ansible.cfg
    │   ├── group_vars
    │   │   └── init
    │   │       ├── vars.yml     <== カスタマイズ
    │   │       └── vault.yml    <== カスタマイズ
    │   ├── hosts
    │   ├── init.yml
    │   └── roles
    │       └── init
    :
    │
    │
    └── tbo_server
        ├── .ansible_vault_pass
        ├── ansible.cfg
        ├── group_vars
        │   └── tbo_server
        │       ├── vars.yml     <== カスタマイズ
        │       └── vault.yml    <== カスタマイズ
        ├── hosts
        ├── roles
        │   ├── apps
        │   ├── certs
        │   ├── httpd
        │   ├── mysql
        │   ├── network
        │   ├── php
        │   ├── ruby
        │   └── system
        │   └── zabbix
        :
        └── tbo_server.yml
```

1) initプレイブックを実行する

```
$ cd init
$ ansible-playbook init.yml --vault-password-file=.ansible_vault_pass
```

2) tbo_serverプレイブックを実行する

``` 
$ cd tbo_server
$ ansible-playbook tbo_server.yml --vault-password-file=.ansible_vault_pass
```

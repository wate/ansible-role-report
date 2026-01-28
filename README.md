report
=================

Generate server reports

OS Platform
-----------------

### Debian

- trixie
- bookworm

Role Variables
--------------

### [defaults/main.yml](defaults/main.yml)

設定方法の詳細については[defaults/main.yml](defaults/main.yml)のサンプルコードなどを参照してください。

#### `report_dir`

レポートの出力先ディレクトリ  
レポートはコントロールノード側に作成されます  
※このディレクトリ内に各ホスト毎のディレクトリを作成しレポートを出力します

#### `report_service`

サービスの稼働状況のフィルター変数

#### `report_disk_usage_dirs`

ディスク使用量を調査するディレクトリのリスト

#### `report_file_searches`

検索対象ファイル情報のリスト

#### `jc_version`

インストールするjcのバージョン

#### `osv_scanner_version`

インストールするosv-scannerのバージョン

### [vars/main.yml](vars/main.yml)

設定値については[vars/main.yml](vars/main.yml)を参照してください。

#### `report_jc_repo`

#### `report_osv_scanner_repo`

Example Playbook
--------------

```yaml
- hosts: servers
  roles:
    - role: report
```

License
--------------

Apache License 2.0

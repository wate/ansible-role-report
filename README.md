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

#### `report_platform`

プラットフォーム情報(オプション)  
※サーバー基本情報レポートの上部に表示されます

#### `report_repository`

リポジトリ情報(オプション)  
※サーバー基本情報レポートの上部に表示されます

#### `report_meta`

メタ情報(オプション)  
※レポートの上部にYAMLフロントマターとして埋め込まれます

#### `report_sbom_dir`

SBOMの出力先ディレクトリ(サーバー上)  
trivy rootfsで生成したCycloneDX形式のSBOMを保存します

#### `report_sbom_filename`

SBOMのファイル名

#### `report_vulnerability_enabled`

脆弱性レポートを生成するかどうか  
生成したSBOMをtrivyで検査し脆弱性レポートを出力します  
無効の場合は既存の脆弱性レポートを削除します  
※初回実行時は脆弱性DB(展開後約1.7GB)のダウンロードが必要です

#### `report_vulnerability_severities`

脆弱性レポートに含める重大度  
trivyの`--severity`に渡します(空の場合はすべての重大度が対象)

#### `report_vulnerability_ignorefile`

除外する脆弱性の定義(任意)  
空の場合は除外設定なし(既存の定義ファイルは削除されます)  
詳細: [Filtering](https://trivy.dev/docs/latest/configuration/filtering/)

#### `report_vulnerability_ignorefile_name`

除外設定のファイル名  
YAML形式の場合は`.trivyignore.yaml`を指定します(拡張子で形式が判定されます)

#### `report_service`

サービスの稼働状況のフィルター変数

#### `report_disk_usage_dirs`

ディスク使用量を調査するディレクトリのリスト

#### `report_file_searches`

検索対象ファイル情報のリスト

#### `jc_version`

インストールするjcのバージョン

### [vars/main.yml](vars/main.yml)

設定値については[vars/main.yml](vars/main.yml)を参照してください。

#### `report_jc_repo`

#### `report_trivy_apt_key_url`

#### `report_trivy_apt_key_download_dest`

#### `report_trivy_apt_key_dest`

Example Playbook
--------------

```yaml
- hosts: servers
  roles:
    - role: report
```

Test
--------------

Moleculeのシナリオは次の3つです。

| シナリオ      | 内容                                                       |
| ------------- | ---------------------------------------------------------- |
| default       | 既定値。SBOMの生成までを検証                               |
| option_vars   | 任意変数(メタ情報など)の反映を検証                         |
| vulnerability | 脆弱性レポートの生成までを検証(初回は脆弱性DBの取得が発生) |

`task`コマンドで実行します。

- `task`: defaultシナリオ
- `task option_vars`: option_varsシナリオ
- `task vulnerability`: vulnerabilityシナリオ
- `task all`: すべてのシナリオ

各シナリオには`collections.yml`と`requirements.yml`を置いてあり、
moleculeの`dependency`ステップで必要なコレクションが自動導入されます。

検証の最後に、目視確認用として生成したSBOMを`molecule-report/<ホスト名>/sbom.cdx.json`へ取得します。

License
--------------

Apache License 2.0

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

#### `report_version`

インストールするバージョン

#### `report_packages`

インストールするパッケージ

#### `report_cfg`

reportの設定

### [vars/main.yml](vars/main.yml)

設定値については[vars/main.yml](vars/main.yml)を参照してください。

#### `report_dependency_packages`

#### `report_root`

#### `report_user`

#### `report_group`

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

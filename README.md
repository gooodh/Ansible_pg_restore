# Ansible_pg_restore

## First, copy the application:

```bash
git clone git@github.com:gooodh/Ansible_pg_restore.git
```
## Install dependencies:
```bash
uv sync
```

## Start playbook command:

### Add the archive and checksum to this path
```bash
roles/postgresql/files/db_mailing_bot_2026-02-07.sql.gz.sha256
roles/postgresql/files/db_mailing_bot_2026-02-07.sql.gz
```
### Add variables
[group_vars](inventory/group_vars/all/all.yml)

```text
pg_version: 16

pg_db_name: mailing_bot
pg_db_user: postgres_bot

pg_dump_file: db_mailing_bot_2026-02-07.sql.gz
pg_dump_sha256: db_mailing_bot_2026-02-07.sql.gz.sha256

pg_restore_dir: /opt/db_restore
```
### Ansible Vault (secrets)
```bash
ansible-vault create group_vars/all/vault.yml
```
```text
pg_db_password: secret
```
### ▶ Run all roles with verbose output:
```bash
ansible-playbook playbooks/start_settings.yml -i inventory/hosts.yml -K --ask-vault-pass
```
### ▶ Run only postgresql:
```bash
ansible-playbook playbooks/start_settings.yml -i inventory/hosts.yml -K --tags postgresql --ask-vault-pass
```
### Connect to the `mailing_bot` database
```bash
sudo -u postgres psql mailing_bot
```

### Check tables
```sql
\dt
```
### Check data
```sql
SELECT * FROM payments;
```

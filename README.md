# Digital Ocean - Laravel

## Run a Playbook

Add `vault.yml`

```bash
$ EDITOR=nano ansible-vault create vault.yml
```

```yml
---
app_name: acme
app_tld: com
global_password: "<passwd>"
sudo_user: cwilby
db_user: db
web_user: web
web_key_name: id_rsa
github_keys: https://github.com/cwilby.keys
github_token: "<token>"
dgto_token: "<token>"
droplet_ssh_pk: "<fingerprint>"
droplet_region: sfo2
droplet_name: acme-sf02-prod
droplet_size: s-2vcpu-4gb
droplet_image: ubuntu-16-04-x64
app_repo_name: laravel
app_repo_owner: laravel
app_repo_branch: master
```

Add `playbook.yml`
```yml
---
- name: Ensure application is live in production.
  hosts: localhost
  vars_files:
    - vault.yml
  roles:
    - cwilby.dgto-laravel
```

Add `requirements.yml`
```yml
---
- src: https://github.com/cwilby/ansible-dgto-laravel.git
  version: master
  name: cwilby.dgto-laravel
```

Install requirements
```yml
$ ansible-galaxy install -r requirements.yml
```

Run playbook
```bash
$ ansible-playbook --ask-become --ask-vault playbook.yml
```

## Dependencies

* [geerlingguy.swap](https://github.com/geerlingguy/ansible-role-swap)
* [geerlingguy.mysql](https://github.com/geerlingguy/ansible-role-mysql)
* [geerlingguy.redis](https://github.com/geerlingguy/ansible-role-redis)
* [geerlingguy.php](https://github.com/geerlingguy/ansible-role-php)
* [geerlingguy.composer](https://github.com/geerlingguy/ansible-role-composer)
* [geerlingguy.nodejs](https://github.com/geerlingguy/ansible-role-nodejs)
* [geerlingguy.nginx](https://github.com/geerlingguy/ansible-role-nginx)
* [geerlingguy.certbot](https://github.com/geerlingguy/ansible-role-certbot)
* [geerlingguy.mysql](https://github.com/geerlingguy/ansible-role-mysql)

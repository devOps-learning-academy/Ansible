# Ansible Galaxy: Real-World Use Case

Ansible Galaxy provides reusable roles and collections. The example below
uses the Galaxy `geerlingguy.nginx` role to configure an Nginx web server.

## Project files

```text
.
├── requirements.yml
├── inventory.ini
└── site.yml
```

## Install Galaxy dependencies

Create `requirements.yml`:

```yaml
---
roles:
	- name: geerlingguy.nginx
		version: "3.2.0"
collections:
	- name: community.general
		version: ">=8.0.0"
```

Install the role and collection:

```bash
ansible-galaxy install -r requirements.yml
```

## Inventory

`inventory.ini`:

```ini
[web]
web-01 ansible_host=192.0.2.10

[web:vars]
ansible_user=ubuntu
```

## Playbook

`site.yml`:

```yaml
---
- name: Configure production web servers
	hosts: web
	become: true
	vars:
		nginx_remove_default_vhost: true
		nginx_vhosts:
			- listen: "80"
				server_name: "example.com"
				root: "/var/www/example"
				index: "index.html"
	roles:
		- geerlingguy.nginx
```

Run the playbook:

```bash
ansible-playbook -i inventory.ini site.yml
```

## Create and publish a custom role

```bash
ansible-galaxy role init roles/web
ansible-galaxy role build roles/web
ansible-galaxy role publish namespace.web --token "$GALAXY_API_KEY"
```

Keep Galaxy tokens in environment variables or Ansible Vault, never in source
control.

N

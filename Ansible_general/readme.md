 # Different Ways to Write an Ansible Inventory
An inventory defines the hosts and groups managed by Ansible. The default inventory file is often named `inventory` or `hosts`.
## 1. INI inventory
```ini
[web]
web01 ansible_host=192.168.1.10 ansible_user=ubuntu
web02 ansible_host=192.168.1.11

[database]
db01 ansible_host=192.168.1.20

[production:children]
web
database
```

Group variables can be declared with `:vars`:

```ini
[web:vars]
ansible_port=22
ansible_python_interpreter=/usr/bin/python3
```

## 2. YAML inventory

```yaml
all:
	children:
	web:
	hosts:
	web01:
		  ansible_host: 192.168.1.10
		  ansible_user: ubuntu
	web02:
		  ansible_host: 192.168.1.11
	database:
	hosts:
	db01:
		  ansible_host: 192.168.1.20
	vars:
	ansible_python_interpreter: /usr/bin/python3
```

## 3. Host ranges in INI

```ini
[web]
web[01:05].example.com

[database]
db-[a:c].example.com
```

## 4. Aliases and connection variables

An alias can differ from the actual host address:

```ini
[web]
frontend ansible_host=web01.example.com ansible_user=deploy
```

## 5. Dynamic inventory

Inventory plugins or scripts can discover hosts from cloud providers and other systems:

```bash
ansible-inventory -i aws_ec2.yml --graph
```

Example inventory-plugin configuration:

```yaml
plugin: amazon.aws.aws_ec2
regions:
	- us-east-1
keyed_groups:
	- key: tags.Environment
	prefix: env
```

## 6. Multiple inventory sources

```bash
ansible-playbook -i inventories/production -i inventories/common site.yml
```

## Validate an inventory

```bash
ansible-inventory -i inventory.ini --list
ansible-inventory -i inventory.ini --graph
```

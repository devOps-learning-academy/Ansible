 # Ansible Roles

Ansible roles provide a reusable, structured way to organize automation. A role can contain tasks, handlers, variables, templates, files, and defaults.

## Typical structure

```text
roles/
└── webserver/
		├── defaults/main.yml       # Low-precedence default variables
		├── vars/main.yml           # Higher-precedence role variables
		├── tasks/main.yml          # Main list of tasks
		├── handlers/main.yml       # Handlers notified by tasks
		├── templates/              # Jinja2 templates (*.j2)
		├── files/                  # Static files
		├── meta/main.yml           # Dependencies and role metadata
		└── README.md
```

## Example role

`roles/webserver/tasks/main.yml`:

```yaml
---
- name: Install nginx
	ansible.builtin.package:
		name: nginx
		state: present

- name: Start and enable nginx
	ansible.builtin.service:
		name: nginx
		state: started
		enabled: true
```

Use the role from a playbook:

```yaml
---
- name: Configure web servers
	hosts: web
	become: true
	roles:
		- webserver
```

Run it with:

```bash
ansible-playbook -i inventory.ini site.yml
```

## Creating and sharing roles

```bash
ansible-galaxy role init roles/webserver
ansible-galaxy install namespace.role_name
```

Keep configurable values in `defaults/main.yml`, use handlers for changes that require a restart, and declare external role dependencies in `meta/main.yml`.

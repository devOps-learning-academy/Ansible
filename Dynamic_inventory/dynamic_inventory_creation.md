# Ansible Dynamic Inventory in Python

This example creates a dynamic inventory script that Ansible can execute to discover hosts.

## 1. Create the inventory script

Save the following as `dynamic_inventory.py`:

```python
#!/usr/bin/env python3
"""Simple Ansible dynamic inventory."""

import json
import sys


INVENTORY = {
	"all": {
		"children": ["web", "db"],
	},
	"web": {
		"hosts": ["web01", "web02"],
		"vars": {
			"ansible_user": "ubuntu",
		},
	},
	"db": {
		"hosts": ["db01"],
		"vars": {
			"ansible_user": "ubuntu",
		},
	},
	"_meta": {
		"hostvars": {
			"web01": {"ansible_host": "192.168.1.10"},
			"web02": {"ansible_host": "192.168.1.11"},
			"db01": {"ansible_host": "192.168.1.12"},
		}
	},
}


def main():
	# Ansible passes --list when it needs the complete inventory.
	# It may pass --host <name> for one host; hostvars are already in _meta.
	if len(sys.argv) == 2 and sys.argv[1] in ("--list", "--host"):
		print(json.dumps(INVENTORY, indent=2))
	elif len(sys.argv) == 3 and sys.argv[1] == "--host":
		print(json.dumps(INVENTORY["_meta"]["hostvars"].get(sys.argv[2], {})))
	else:
		print("Usage: dynamic_inventory.py --list | --host <hostname>", file=sys.stderr)
		sys.exit(1)


if __name__ == "__main__":
	main()
```

> Replace the host names, IP addresses, and SSH user with your own values.

## 2. Make the script executable

On Linux or macOS, run:

```bash
chmod +x dynamic_inventory.py
```

On Windows, run it through Python instead of using `chmod`:

```powershell
python dynamic_inventory.py --list
```

## 3. Test the script

Check that it returns valid JSON:

```bash
python3 dynamic_inventory.py --list
python3 dynamic_inventory.py --host web01
```

## 4. Use it with Ansible

Test the inventory and display the discovered hosts:

```bash
ansible-inventory -i ./dynamic_inventory.py --list
ansible-inventory -i ./dynamic_inventory.py --graph
```

Run a playbook with the dynamic inventory:

```bash
ansible-playbook -i ./dynamic_inventory.py site.yml
```

## 5. Optional: configure `ansible.cfg`

Set the script as the default inventory:

```ini
[defaults]
inventory = ./dynamic_inventory.py
```

Then you can run:

```bash
ansible all -m ping
```

The script can later be extended to query a cloud API, database, or CMDB instead of using the hard-coded `INVENTORY` dictionary. Keep the output in Ansible's JSON inventory format.

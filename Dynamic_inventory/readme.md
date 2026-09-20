 # Ansible Dynamic Inventory for AWS EC2

Use Ansible's AWS EC2 inventory plugin to discover running EC2 instances dynamically.

## Requirements

- Ansible and the `amazon.aws` collection
- AWS credentials configured through the AWS CLI, environment variables, or an IAM role
- Network access and an SSH key for the target instances

```bash
ansible-galaxy collection install amazon.aws
aws configure
```

## Inventory file

Save this as `aws_ec2.yml`:

```yaml
plugin: amazon.aws.aws_ec2
regions:
	- us-east-1                 # Change to your AWS region
filters:
	instance-state-name: running
keyed_groups:
	- key: tags.Name
		prefix: tag
	- key: instance_type
		prefix: type
compose:
	ansible_host: public_ip_address
```

The `compose` setting makes Ansible connect using each instance's public IP. For private instances, use `private_ip_address` instead and ensure the network is reachable.

## Test the inventory

```bash
ansible-inventory -i aws_ec2.yml --graph
ansible-inventory -i aws_ec2.yml --list
```

## Connect to EC2 instances

Create `ansible.cfg`:

```ini
[defaults]
inventory = aws_ec2.yml
private_key_file = ~/.ssh/my-ec2-key.pem
host_key_checking = False
remote_user = ec2-user
```

Ubuntu AMIs commonly use `ubuntu` instead of `ec2-user`.

```bash
ansible all -m ping
ansible tag_web -m setup
ansible-playbook site.yml
```

Limit access with an IAM policy that allows only the required EC2 discovery actions, such as `ec2:DescribeInstances` and `ec2:DescribeRegions`.

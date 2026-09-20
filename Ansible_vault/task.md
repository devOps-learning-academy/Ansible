## Task: Create an Ansible Playbook Using Ansible Vault for AWS Credentials

Write an Ansible playbook that performs an AWS operation, such as creating an
S3 bucket or provisioning an EC2 instance. AWS credentials must be stored in an
encrypted Ansible Vault file, not in the playbook or source code.

### Requirements

1. Create `group_vars/all/vault.yml` with `ansible-vault create` and add these
	placeholders:

	```yaml
	vault_aws_access_key: "<AWS_ACCESS_KEY_ID>"
	vault_aws_secret_key: "<AWS_SECRET_ACCESS_KEY>"
	vault_aws_session_token: "<AWS_SESSION_TOKEN_IF_REQUIRED>"
	vault_aws_region: "<AWS_REGION>"
	```

2. Create `aws_task.yml` with a play and at least one AWS module.
3. Pass the vaulted variables to the module where required. Use this pattern:

	```yaml
	access_key: "{{ vault_aws_access_key }}"
	secret_key: "{{ vault_aws_secret_key }}"
	session_token: "{{ vault_aws_session_token | default(omit) }}"
	region: "{{ vault_aws_region }}"
	```

4. Never hard-code real credentials, commit an unencrypted credentials file, or
	display credentials in task output.
5. Document the AWS operation and the IAM permissions required to run it.

### Suggested commands

```bash
ansible-vault create group_vars/all/vault.yml
ansible-playbook aws_task.yml --ask-vault-pass
```

For automation, use a protected vault-password file or secret-management system
instead of exposing the password in shell history. Verify that the playbook
runs successfully and that the credentials remain encrypted.

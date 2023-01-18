# ansible_pull_tutorial
This is an example of ansible pull

## Prepare Target PCs (ubuntu)

### Install necessary packages ... git and ansible

`$ sudo apt install git ansible cron`

### Run `ansible-pull` where U specifies HTML URL

`$ sudo ansible-pull -U https://github.com/nospam1961/ansible_pull_tutorial.git`

## Ansible Vault

### Create ~/.vault_key file with the password and chmod to 600

`$ echo "My Secret Secure Password" > ~/.vault_key`

`$ chmod 600 ~/.vault_key`

### Encrypt tasks/files/sudoers_ansible

`$ ansible-vault encrypt --vault-password-file ~/.vault_key ./tasks/files/sudoers_ansible`

### Decrypt

`$ ansible-vault decrypt --vault-password-file ~/.vault_key ./tasks/files/sudoers_ansible`

### View

`$ ansible-vault view --vault-password-file ~/.vault_key ./tasks/files/sudoers_ansible`

### Edit

`$ ansible-vault edit --vault-password-file ~/.vault_key ./tasks/files/sudoers_ansible`

### Rekey

`$ ansible-vault rekey --vault-password-file ~/.vault_key ./tasks/files/sudoers_ansible --new-vault-password-file ~/.vault_key_new`

## Run ansible-pull without passing ansible vault key - WILL GENERATE ERROR as sudoers_ansible is encrypted

`$ sudo ansible-pull -U https://github.com/nospam1961/ansible_pull_tutorial.git -i "$(hostname --short),"`

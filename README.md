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

## Run ansible-pull with ansible vault key (MAKE SURE ~/.vault_key IS COPIED TO EVERY SERVER / WS THAT WILL RUN ansible-pull)

`$ sudo ansible-pull -U https://github.com/nospam1961/ansible_pull_tutorial.git --vault-password-file ~/.vault_key -i "$(hostname --short),""`

## Since cron job runs under user ansible

### Copy .vault_key to ansible home

`$ sudo cp ~/.vault_key /home/ansible/.vault_key`

### Change .vault_key to 600

`$ sudo chmod 600 /home/ansible/.vault_key` 

### Change owner of .vault_key in ansible home to be ansible user

`$ sudo chown ansible:ansible /home/ansible/.vault_key`

### Permissions and owner should be changed

`$ sudo ls -la /home/ansible/.vault_key`

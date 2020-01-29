# Ansible Playbooks

`-f 20` runs the playbook on 20 servers concurrently

# Execute locally

## Check upgradable packages:
- server_admin/check_updates.yml

Only works on Ubuntu 16
```bash
ansible-playbook -f 20 --ask-vault-pass -i ../hosts check_updates.yml
```

## Upgrade packages and kernel:
- server_admin/update_hosts.yml

```bash
time ansible-playbook -f 20 --ask-vault-pass update_hosts.yml -i ../hosts
```

View upgradable packages per server:
```bash
cat /tmp/upgradable-pkgs/hostname.json | jq .
```

View upgradable packages on all servers:
```bash
cat /tmp/upgradable-pkgs/* | jq .
```

## Add etc backup script:
- server_admin/add_etc_backup_script.yml

```bash
ansible-playbook -f 20 --ask-vault-pass -i ../hosts add_etc_backup_script.yml
```

## Change user password safely

- server_admin/change_user_pass.yml

This playbook changes the users password and adds a crontab which will revert the change if one is locked out. Set the crontabs atleast 20min after the server time.


- server_admin/remove_pass_revert_cron.yml

Once your new passwords have been changed and you are not locked out of the server. Change all the vault passwords with the new password and run the playbook to delete the passwors revert cron.

### Vagrant - Test locally

```bash
cd server_admin
vagrant up
vagrant ssh
ip a
passwd vagrant
# Insert the ip and password in to hosts
# Edit cancel_passwd_revert_cron.yml and change_user_pass.yml to run on the correct host.
ansible-playbook -f 20 --ask-vault-pass -i ../hosts change_user_pass.yml
ansible-playbook -f 20 --ask-vault-pass -i ../hosts remove_passwd_revert_cron.yml
```

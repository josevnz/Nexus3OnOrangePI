# Secrets

The Nexus 3 administrator password, among others are stored into a Ansible vault encrypted file.

```shell
[josevnz@dmaf5 vault]$ ansible-vault encrypt nexus_password.enc
New Vault password: 
Confirm New Vault password: 
Encryption successful
```

File contents are encrypted:

```text
[josevnz@dmaf5 ansible]$ cat vault/nexus_password.enc 
$ANSIBLE_VAULT;1.1;AES256
64623430366534373465356561616662313761646164653965383739323761336637363863326265
6161643936303662656535336434643237643135383936610a353836316430356137303735343462
63326364643365663764393235386534646463326136643435323932303762616565366438663336
3132333231373439610a323734663634346239663736666163313734316161336630303533386633
30343138393362333936383135363233346665663964653733316562363538616166343863363439
37623139326133656234616239303539626437366332636231343637386331346266623162373037
386433313766383161363735653637333962
```

```shell
[josevnz@dmaf5 ansible]$ ansible-vault view vault/nexus_password.enc 
Vault password: 
admin_password: XXX
client_password: YYY
```

Then you keep your password file on a safe location, and you can tell Ansible to un-encrypt the contents like this:

```shell
[josevnz@dmaf5 ansible]$ cd ansible
[josevnz@dmaf5 ansible]$ ansible-playbook --inventory  inventories --extra-vars @vault/nexus_password.enc --vault-password-file $HOME/vault/ansible_vault_pass site.yaml
```

## Documentation

* [Ansible's playbooks secrets](https://www.redhat.com/sysadmin/ansible-playbooks-secrets)
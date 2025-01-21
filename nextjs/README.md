### Nextjs deploy template.
**how it works:** \
On push to main, build application in the pipeline.
Backup *current* symlink, if it exists, to the backups folder.
Download latest artifact from pipeline and extract it to the *out* directory.
Set the *out* directory as the *current* directory.

**how to use**: \
Create pipeline with github-pipeline.yml temlate.
Create Github PAT with read privelleges on action.

1. Install ansible dependencies:
```bash
ansible-galaxy install ansible-role-nvm
```
 
3. Fill common_vars and vault.yml
4. Encode vault for security (optional when debug)
```bash
ansible-vault encrypt vars/vault.yml
```
6. Install all nginx, nginx-config and node
```bash
ansible-playbook -i inventory.ini dependencies.yml
```

Deploy
```bash
ansible-playbook -i inventory.ini deploy.yml
```

Rollback
```bash
ansible-playbook -i inventory.ini rollback.yml
```

*todo:* \
move nginx config to external file \
test rollback \
switch backups to versions instead of timestamps \
switch from curl to some kind of github collection

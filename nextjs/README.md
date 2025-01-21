### Nextjs deploy template.
**how it works:**
On push main build application in pipeline.
Backup current(symlink) if exists to backups folder.
Download last artifact from pipelines and extract to out.
Make out = current.

**how to use**:
Create pipeline with github-pipeline.yml temlate.
Create Github PAT with read privelleges on action.

1. Install ansible dependencies:
`ansible-galaxy install ansible-role-nvm`
 
2. Fill common_vars and vault.yml
3. Encode vault for security (optional when debug)
`ansible-vault encrypt vault.yml`
4. Install all nginx, nginx-config and node
`ansible-playbook -i inventory.ini dependencies.yml`

Deploy
`ansible-playbook -i inventory.ini deploy.yml`
Rollback
`ansible-playbook -i inventory.ini rollback.yml`

*todo:*
move nginx config to external file
test rollback
switch backups to versions instead of timestamps
switch from curl to some kind of github collection

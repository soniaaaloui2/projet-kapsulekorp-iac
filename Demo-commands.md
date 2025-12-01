# 🚀 KapsuleKorp Ansible - Commandes de Démonstration

# 1. Show structure
tree -L 3

# 2. Check syntax
ansible-playbook site.yml --syntax-check

# 3. List tasks
ansible-playbook site.yml --list-tasks

# 4. Ping both VMs
ansible all -m ping --ask-vault-pass -K

# 5. SSH web server
ssh -p 2222 sonia@127.0.0.1
# Inside: systemctl status nginx php8.4-fpm
# Type: exit

# 6. SSH database server
ssh -p 2223 sonia@127.0.0.1
# Inside: sudo systemctl status mysql 

# Type: exit

# 7. Show git history
git log --oneline

# 8. Show nginx role
cat roles/nginx/tasks/main.yml

# 9. Show vault
cat group_vars/all/vault.yml

# 10. Show readme
cat README.md

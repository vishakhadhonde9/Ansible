# Ansible Vault -
- Ansible Vault is a feature that allows you to encrypt secrets like:
    - Passwords (e.g., MySQL, SSH)
    - API keys
    - Certificates
    - Any sensitive data inside files
    - So you can store secrets safely in version control without exposing them.
 
## 1. Encrypt a file

  ansible-vault encrypt mypass.txt

## 2. Decrypt a file

  ansible-vault decrypt mypass.txt

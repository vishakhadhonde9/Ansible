# Ansible Vault -
- Ansible Vault is a feature that allows you to encrypt secrets like:
    - Passwords (e.g., MySQL, SSH)
    - API keys
    - Certificates
    - Any sensitive data inside files
    - So you can store secrets safely in version control without exposing them.
 
## 1. Encrypt a file

  ansible-vault encrypt mypass.yml

## 2. Decrypt a file

  ansible-vault decrypt mypass.yml


## Credentials (mypass.yml)
   
    username: myuser
    password: mysecurepassword

## Playbook File -

        - name: Secret MySQL Setup
          hosts: myserver
          become: yes
        
          vars_files:
            - mypass.yml
        
          tasks:
            - name: Update yum packages
              yum:
                name: '*'
                state: latest
        
            - name: Install pip
              yum:
                name: python3-pip
                state: present
        
            - name: Install Python MySQL Module
              pip:
                name: PyMySQL
        
            - name: Install MariaDB
              yum:
                name: mariadb105-server
                state: present
        
            - name: Start MariaDB service
              service:
                name: mariadb
                state: started
        
            - name: Create MySQL user
              community.mysql.mysql_user:
                name: "{{ username }}"
                password: "{{ password }}"
                login_unix_socket: /var/lib/mysql/mysql.sock
                check_implicit_admin: yes
                update_password: always
                state: present
        

ansible-playbook -i myhost.ini secret.yml --ask-vault-pass











# To install Packages on Remote Server -
- Create remote server (EC2 inatsnce).
- Copy keypair of remote server into ansible server.

      scp -i ansible_keypair.pem localpath_to_remotekeypair.pem user@ansible_server_ip

- Connnect to Ansible server and verify keypair is copied.c
- Add Permissions to keypair.

    sudo chmod 400 keypair.pem

- Create new/Change existing Inventory file.

     [webservers]
      your_remote_server_ip ansible_user=your_ssh_user

- Create playbook file

        - name: Install Nginx on remote server
          hosts: webservers
          become: true
          tasks:
            - name: Install Nginx
              apt:
                name: nginx
                state: present
        
            - name: Ensure Nginx is running
              service:
                name: nginx
                state: started
                enabled: yes

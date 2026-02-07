# To install Packages on Remote Server -
- Create remote server (EC2 inatsnce).
- Copy keypair of remote server into ansible server.

      scp -i ansible_keypair.pem localpath_to_remotekeypair.pem user@ansible_server_ip:destination

      scp -i ./Downloads/ansible.pem ./Downloads/ansible.pem ubuntu@54.204.253.186:/home/ubuntu/



- Connnect to Ansible server and verify keypair is copied.c
- Add Permissions to keypair.

    sudo chmod 400 keypair.pem

- Create new/Change existing Inventory file.

           [webservers]
            your_remote_server_ip ansible_user=your_ssh_user ansible_private_key_file=keypair.pem

- Create playbook file

        - name: Install Nginx on remote server
          hosts: webservers
          become: true
          tasks:
            - name: apt update
              shell: 'apt update'
            - name: Install Nginx
              apt:
                name: nginx
                state: present
        
            - name: Ensure Nginx is running
              service:
                name: nginx
                state: started
                enabled: yes

# Remote Server with different OS -
## Method -1] 

            - name: Install Nginx on multiple Linux distros
              hosts: webservers
              become: true
              tasks:
                - name: Install Nginx (Debian-based)
                  apt:
                    name: nginx
                    state: present
                  when: ansible_os_family == "Debian"
            
                - name: Install Nginx (RHEL-based)
                  yum:
                    name: nginx
                    state: present
                  when: ansible_os_family == "RedHat"
            
                - name: Ensure Nginx is running and enabled
                  service:
                    name: nginx
                    state: started
                    enabled: yes


# Method-2]


                  - name: Install and manage Nginx on Ubuntu and Amazon Linux
                    hosts: webserver
                    become: true
                    gather_facts: true
                  
                    tasks:
                      - name: Install Nginx on Ubuntu
                        apt:
                          name: nginx
                          state: present
                          update_cache: true
                        when: ansible_facts['distribution'] == "Ubuntu"
                  
                      - name: Install Nginx on Amazon Linux
                        yum:
                          name: nginx
                          state: present
                        when: ansible_facts['distribution'] == "Amazon"
                  
                      - name: Start and enable Nginx service
                        service:
                          name: nginx
                          state: started
                          enabled: true


#### Add env var to avoid key checking:

            export ANSIBLE_HOST_KEY_CHECKING=False

            

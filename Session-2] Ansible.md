# item_with -

        - name: Setup LEMP stack
          hosts: webservers
          become: yes
        
          tasks:
            - name: Install web server packages
              apt:
                name: "{{ item }}"
                state: present
                update_cache: yes
              with_items:
                - nginx
                - mariadb-server
                - php


# Loop -
- Loops are used to repeat a task multiple times with different items.

- name: Setup LEMP stack
          hosts: webservers
          become: yes
        
          tasks:
            - name: Install web server packages
              apt:
                name: "{{ item }}"
                state: present
                update_cache: yes
              loop:
                - nginx
                - mariadb-server
                - php

# Create File and Directory -
- To create a file or directory in Ansible, you use the file module.

        - name: Create files and directories
          hosts: webservers
          become: yes
          tasks:
        
            - name: Create a directory for logs
              file:
                path: /var/www/myapp/logs
                state: directory
                mode: '0755'
        
            - name: Create a config file
              file:
                path: /var/www/myapp/config.yaml
                state: touch
                mode: '0644'

## Copy File -

        - name: Copy a file to remote host
          copy:
            src: /path/on/control/machine/file.txt
            dest: /path/on/remote/machine/file.txt
          


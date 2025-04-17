# Variables -
- Variables are used to store values.

        - name: My First Playbook
          hosts: localhost
          become: true
          connection: local
        
          vars:
            my_port: 90
            my_path: /var/www/html/myweb
        
          tasks:
            - name: Install Nginx
              apt:
                name: nginx
                state: present
                update_cache: true
        
            - name: Start Nginx service
              service:
                name: nginx
                state: started
                enabled: true
        
            - name: Create a directory for the website
              file:
                path: "{{ my_path }}"
                state: directory
                
            - name: Copy index.html to web directory
              copy:
                src: ./index.html
                dest: "{{ my_path }}/index.html"
        
                
            - name: Reload Nginx to apply new configuration
              service:
                name: nginx
                state: reloaded

# Handlers-
- A handler is a special kind of task that only runs when notified by another task.
- Suppose you changed configuration file so in that case you need to restart the service; for that purpose we can use handlers.
- A handler is a special kind of task in Ansible that is triggered only when notified by another task.


        - name: Install Nginx
          apt:
            name: nginx
            state: present
        
        - name: Copy Nginx config
          copy:
            src: nginx.conf
            dest: /etc/nginx/nginx.conf
          notify: Restart Nginx
        
        handlers:
          - name: Restart Nginx
            service:
              name: nginx
              state: restarted


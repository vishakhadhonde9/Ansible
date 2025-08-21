# Variables -
- Variables are used to store values.
- Template is required if you are using variable for copying purpose.

                - name: myplay1
                  hosts: localhost
                  become: true
                  connection: local
                
                  vars:
                    my_port: 90
                    my_path: /var/www/html/myweb
                
                  tasks:
                    - name: Install nginx
                      apt:
                        name: nginx
                        state: present
                        update_cache: true
                
                    - name: Start nginx service
                      service:
                        name: nginx
                        state: started
                        enabled: true
                
                    - name: Create a directory
                      file:
                        path: "{{ my_path }}"
                        state: directory
                
                    - name: Copy index.html to web directory
                      copy:
                        src: ./index.html
                        dest: "{{ my_path }}/index.html"
                
                    - name: Copy nginx configuration file
                      template:
                        src: ./mynginx.conf
                        dest: /etc/nginx/sites-enabled/default
                
                    - name: Reload nginx
                      service:
                        name: nginx
                        state: reloaded



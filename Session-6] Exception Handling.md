# Exception/Error Handling -
- Exception handling refers to the ability to manage errors, exceptions, and unexpected conditions during playbook execution, allowing you to recover gracefully or take specific actions when things go wrong.

# Block, rescue and always -

## 1. block – The main code (try block)
- This is where you put the tasks that you want to try to run.
- If anything fails inside the block, Ansible jumps to the rescue section.

## 2. rescue – Error handler (catch block)
- This section runs only if something in the block fails.
- You can use it to send a message, try a different command, or fix something.

## 3. always – Always runs (finally block)
- This section runs no matter what — whether the block was successful or not.
- Great for cleanup or status reporting.


            - name: myplay1
              hosts: localhost
              become: true
              connection: local
            
              tasks:
                - block:
                    - name: Install ambiguous package
                      apt:
                        name: nginx
                        state: present
            
            
                    - debug:
                        msg: "In block"
            
                  rescue:
                    - name: Install nginx using apt (rescue)
                      apt:
                        name: nginx
                        state: present
            
                    - debug:
                        msg: "In rescue"
            
                  always:
                    - debug:
                        msg: "In always"

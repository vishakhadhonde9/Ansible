# Ansible Galaxy -
- Ansible Galaxy is a community hub for sharing and discovering Ansible roles, collections, and automation content.
- It's a great place to find reusable automation code like your play store.

## Role -
- An Ansible role is a structured way to organize playbook content—like tasks, variables, templates, and handlers—into reusable components.

### Create a Role -

    ansible-galaxy init role_name

## Structure of Role -


        myrole/
        ├── defaults/
        │   └── main.yml           # Default variables
        ├── files/
        │   └── ...                # Static files (copied to remote host)
        ├── handlers/
        │   └── main.yml           # Handlers triggered by notify
        ├── meta/
        │   └── main.yml           # Role metadata (dependencies, author, etc.)
        ├── tasks/
        │   └── main.yml           # Main list of tasks
        ├── templates/
        │   └── ...                # Jinja2 templates
        ├── vars/
        │   └── main.yml           # Variables with higher precedence


## Add Tasks to Install NGINX -

      - name: Install NGINX
        apt:
          name: nginx
          state: present
          update_cache: yes
        become: true
      
      - name: Ensure NGINX is running
        service:
          name: nginx
          state: started
          enabled: true

## Playbook file

      - name: Install NGINX using custom role
        hosts: localhost
        become: true
        roles:
          - role_name



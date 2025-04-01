# Introduction -
- Ansible is an open-source automation tool used for configuration management, application deployment, and orchestration.
- It simplifies IT operations by automating repetitive tasks without requiring agents on managed systems.
- Instead of manually setting up servers, installing software, or updating configurations, you can use Ansible to do it automatically with simple commands.

 # Why Ansible -
- No manual work – Automates tasks like software installation, updates, and server setup
- No agents needed – Uses SSH, so no extra software is required on remote machines
- Easy to use – Uses YAML playbooks, which are simple to write and read
- Works everywhere – Can manage Linux, Windows, cloud servers (AWS, Azure, GCP), and even containers


# Ansible Architecture -

### 1] Control Node (Ansible Server) -
- The machine where Ansible is installed and executed.
- Sends commands to managed nodes over SSH or WinRM.
### 2️] Managed Nodes (Target Machines) -
- The servers or slaves that Ansible manages.
- No need for Ansible installation on these nodes.

### 3] Inventory File -
- The Ansible inventory file defines the managed nodes (target machines) that Ansible controls.
- It lists IP addresses or hostnames of remote servers and groups them for easier management.
- The default inventory file is located at:

  /etc/ansible/hosts
  
- Ansible inventory files can be in:
    - INI format (.ini) – Simple and widely used
    - YAML format (.yaml or .yml) – Structured and flexible

##### Custom Inventory Files -
- A custom inventory file is a user-defined inventory that specifies managed hosts instead of using the default inventory file (/etc/ansible/hosts).


### 4] Playbook File - 
- An Ansible Playbook is a YAML file that contains a set of instructions (tasks) to automate IT operations like:
✅ Installing software
✅ Managing configurations
✅ Deploying applications
✅ Restarting services

##### Structure of a Playbook -
- A playbook consists of:
   - Hosts → Which machines to run on
   - Tasks → What actions to perform
   - Modules → Built-in Ansible tools for automation


         - name: Install Nginx on Web Servers
           hosts: web_servers
           become: yes  # Run as root (sudo)
           tasks:
             - name: Install Nginx
               apt:
                 name: nginx
                 state: present


name: → Describes the playbook’s purpose
hosts: → The group of servers where it runs (from the inventory file)
become: yes → Runs the tasks with sudo privileges
tasks: → List of actions to perform
apt: → Installs software (specific to Ubuntu/Debian)

###### Running a Playbook -

    ansible-playbook -i custom_inventory.ini install_nginx.yml


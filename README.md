# Simple Linux System management using ansible

## Step 1: Prerequisites
Before you begin, make sure you have Ansible and sshpass installed on your system. You can install them using the following command:

```bash
sudo apt install ansible sshpass
```
##  Step 2: Create Inventory File (servers.ini)

Create a file named servers.ini in a directory of your choice. This file will store the IP addresses of the servers you want to manage. Edit the file to include the following content:


```
[my_servers]
192.168.0.65
192.168.0.66
```
## Step 3: Create Ansible Playbook (commands.yml)

Create another file named commands.yml in the same directory. This file will contain the Ansible playbook that executes commands on the servers. Edit the file and paste the following content for running commands using the command module:

```yaml
---
- name: Run a command using the command module
  hosts: my_servers
  become: yes
  vars:
    ansible_user: user
    ansible_ssh_pass: user
    ansible_become_pass: user
    ansible_become: yes
    ansible_become_method: sudo
  tasks:
    - name: Execute a command
      command: sudo apt install -y cmatrix
```
Alternative Process with apt Module
If you prefer to use the apt module for managing software, you can use the following content in commands.yml:

```yaml

---
- name: Install software
  hosts: my_servers
  become: yes
  vars:
    ansible_user: user
    ansible_ssh_pass: user
    ansible_become_pass: user
    ansible_become: yes
    ansible_become_method: sudo
  tasks:
    - name: Install the software
      apt:
        name: cmatrix
        state: present
```
## Step 4: Running the Ansible Playbook

Open a terminal and navigate to the directory where you saved the servers.ini and commands.yml files.

Run the following command to execute the Ansible playbook and perform the specified tasks on the servers:

```bash
ansible-playbook -i servers.ini commands.yml
```
Ansible will read the inventory file (servers.ini), connect to the servers, and perform the tasks specified in the playbook (commands.yml).

## Example Output
 ansible-playbook -i servers.ini ansible_send_commands_other.yml

PLAY [Run a command using the command module] **********************************************

TASK [Gathering Facts] *********************************************************************
ok: [192.168.0.65]
ok: [192.168.0.66]

TASK [Execute ls command] ******************************************************************
changed: [192.168.0.65]
changed: [192.168.0.66]

PLAY RECAP *********************************************************************************
192.168.0.65               : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.0.66               : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0



### Note
Please make sure you have previously at least tried to login to the server via ssh ie. the devices must be added to the hosts file. Try ssh into the devies once to make sure that is the case

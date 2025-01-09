
Getting Started with Ansible

This guide will take you step-by-step through everything you need to get started with Ansible, from installation to running your first command. Follow along, and you'll be automating your infrastructure in no time!

Prerequisites

Before starting, make sure you have the following:

1. Linux/MacOS/Windows (with WSL installed) – Ansible runs on Unix-based systems, but it can work on Windows with WSL (Windows Subsystem for Linux).
2. SSH Access to a Remote Server – Ansible manages servers using SSH. Make sure you can SSH into the server from your terminal.
3. Python Installed – Ansible requires Python to run. Most systems already have it installed.

---

Step 1: Install Ansible

For Linux (Ubuntu/Debian):

sudo apt update
sudo apt install ansible

For macOS:

brew install ansible

For Windows (with WSL):

Follow this guide (https://docs.ansible.com/ansible/latest/installation_guide/installation_windows.html) to install Ansible via WSL.

---

Step 2: Verify Installation

Once installed, check if Ansible is working by running the following command:

ansible --version

You should see output like this:

ansible 2.x.x
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/usr/share/ansible']

---

Step 3: Set Up Your Inventory

Ansible uses an inventory to know which servers to manage. Let’s create a simple inventory file. 

Create a file called hosts in your working directory:

touch hosts

Now, add the following content to the hosts file:

[local]
localhost ansible_connection=local

This tells Ansible that you will be managing your local machine for now.

---

Step 4: Run Your First Ansible Command

Now, let’s ping your machine to make sure Ansible is connected properly.

Run the following command:

ansible local -m ping -i hosts

Explanation:
- local is the name of the group in your hosts file.
- -m ping specifies the "ping" module, which simply checks if Ansible can reach the server.
- -i hosts tells Ansible where your inventory file is located.

You should see an output like this:

localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

---

Step 5: Create a Simple Playbook

Playbooks in Ansible define the tasks to be executed. Let’s create a basic playbook that installs curl on your local machine.

1. Create a file called playbook.yml:

touch playbook.yml

2. Add the following content to the playbook.yml file:

---
- name: Install curl on local machine
  hosts: local
  become: yes
  tasks:
    - name: Install curl
      apt:
        name: curl
        state: present

Explanation:
- name: Describes the task.
- hosts: local: Specifies the group to run this task on (your local machine).
- become: yes: Runs the task with elevated privileges (root access).
- tasks: The list of tasks to run, which in this case installs curl.

---

Step 6: Run the Playbook

Now that you’ve written your first playbook, it’s time to run it:

ansible-playbook playbook.yml -i hosts

Explanation:
- ansible-playbook: The command to run a playbook.
- playbook.yml: The file containing the playbook to execute.
- -i hosts: Points to the inventory file.

If successful, you should see an output like this:

PLAY [Install curl on local machine] ********************************************************************************************************

TASK [Install curl] **************************************************************************************************************************
ok: [localhost]

PLAY RECAP ***********************************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

This indicates that curl has been installed on your machine.

---

Step 7: Conclusion

Congratulations! You’ve now installed Ansible, created an inventory, run your first command, and created your first playbook. With these basic commands, you can start automating tasks and managing servers. 

Next, you can explore more advanced Ansible features like:
- Managing multiple servers
- Using Ansible roles for better organization
- Writing more complex playbooks

Happy automating with Ansible!


# Ansible Getting Started Guide

## Introduction
Ansible is a simple and powerful automation tool that can help you manage configurations, deployments, and more, across a wide variety of systems. It uses human-readable YAML files to define automation tasks and can be used to manage servers, applications, and services. In this guide, we’ll walk through setting up Ansible on your local machine and running your first command to automate tasks.

## Requirements

- Ansible installed on your local machine
- A basic understanding of the command line
- (Optional) AWS EC2 instance for a real-world scenario demo

## Steps to get started with Ansible

1. **Install Ansible**

   On Ubuntu-based systems:
   ```
   sudo apt update
   sudo apt install ansible
   ```

   On macOS (using Homebrew):
   ```
   brew install ansible
   ```

2. **Create Your First Ansible Playbook**

   Let's start by creating a simple playbook. Create a file named `playbook.yaml` with the following content:

   ```yaml
    ---
    - name: Install Nginx web server
      become: yes
      hosts: all
      tasks:
      - name: Ensure Nginx is installed
        yum:
          name: nginx
          state: present
   ```

   This playbook will install Nginx on your local machine using the `apt` module.

3. **Run the Playbook**

   Open a terminal and navigate to the directory where you saved `playbook.yaml
   `. Then run:

   ```
   ansible-playbook playbook.yaml
   
   ```

   You should see Ansible connecting to your localhost and installing Nginx.

4. **Using Ansible with AWS EC2**

   To use Ansible with an EC2 instance, you can use the following:

   - First, make sure you have an EC2 instance running and accessible via SSH.
   - Then, create a new file called `hosts.ini` with the IP address of your EC2 instance:

     ```
     [ec2]
     54.123.45.67 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/my-ec2-key.pem
     ```

   - Now, update the playbook to install a package (e.g., `nginx`) on the EC2 instance instead of `localhost`. Modify your `playbook.yaml
   ` like this:

     ```yaml
     ---
     - name: Install Nginx web server on EC2
       hosts: ec2
       tasks:
         - name: Ensure Nginx is installed
           apt:
             name: nginx
             state: present
     ```

5. **Run the Playbook on EC2**

   Run the playbook on the EC2 instance with the following command:

   ```
   ansible-playbook -i hosts.ini playbook.yaml
   
   ```

   This command will apply the playbook to your EC2 instance, installing Nginx on it.

## Helpful Ansible Commands

Here are some commonly used Ansible commands:

- `ansible --version` - Check the version of Ansible installed
- `ansible-playbook playbook.yaml` - Run an Ansible playbook
- `ansible -m ping localhost` - Ping localhost to test connectivity
- `ansible-playbook -i hosts.ini playbook.yaml --check` - Perform a dry run of a playbook

## Next Steps

- Learn more about writing complex playbooks and tasks
- Explore using Ansible with multiple EC2 instances or other cloud providers
- Automate entire server setups and application deployments
- Integrate Ansible with CI/CD pipelines for automatic configuration management


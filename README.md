# Ansible Real-Time Project

## Overview
This project is based on my learning and practice with Ansible automation on AWS.  
I worked on creating EC2 instances, setting up passwordless authentication, and automating shutdowns using conditionals.  
All tasks were done from my Ansible control node using connection: local.

---

## Task 1 – Create EC2 Instances Using Loops
- Created three EC2 instances on AWS:
  - Two Ubuntu instances
  - One Amazon Linux instance
- Used Ansible loops to create multiple instances in one playbook.
- Used connection: local so the playbook runs directly from the control node without SSH to remote hosts.
- Verified instance creation from the AWS console.

Concepts used: loops, amazon.aws.ec2_instance, connection: local

---

## Task 2 – Passwordless Authentication Setup
Steps:
  1. Generate SSH keys on control node using:
     ```bash
      ssh-keygen -t rsa
	 
  2. Copied the public key to each EC2 instance using :
     ```bash
     ssh-copy-id -i ~/.ssh/id_rsa.pub -o "IdentityFile=~/.ssh/devops.pem" ec2-user@<instance-ip>
	  
  3. Added host entries in the SSH config file for easy login:
     ```bash
      Host ec2-instance-1
      HostName <instance-ip>
      User ec2-user
      IdentityFile ~/.ssh/devops.pem
	  
  4. After setup, I was able to connect using aliases like:
     ssh ec2-instance-1
	 
Concepts used: ssh-keygen, ssh-copy-id, passwordless SSH, SSH config

---

## Task 3 – Automate Shutdown of Ubuntu Instances
- Automated the shutdown of Ubuntu EC2 instances only using Ansible conditionals.
- Used when condition with ansible_facts to check the OS type before running the shutdown task.
- Amazon Linux instance was skipped automatically.

Concepts used: when, ansible_facts, conditional execution

---

## Tools and Technologies
- Ansible for automation  
- AWS EC2 for cloud instances  
- YAML for playbook structure  
- SSH key authentication for secure access

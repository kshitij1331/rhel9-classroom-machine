# Simple Classroom Server Setup

This is a simple classroom server setup based on a real RHCSA exam server.

## Configuration Overview

- NTP is configured
- HTTPD is configured
- NFS is configured

## Before Running the Script

1. Change the interface name in `./classroom/classroom/network/config.yml` file.
2. Change the hosts in `./classroom/classroom.yml`.

## How to Run the Script

1. Create a new RHEL 9 machine with yum locally configured on it with network adapters.
2. Set hostname and domain name.
    ```bash
    hostnamectl set-hostname classroom
    vim /etc/hosts
    # Add the following line:
    172.25.250.254 content.example.com classroom
    ```

3. Install Ansible.
    ```bash
    yum install ansible -y
    ```

4. Configure Ansible.
    ```bash
    pwd
    /root

    mkdir ansible
    cd ansible
    vim ansible.cfg
    ```
    Add the following content to `ansible.cfg`:
    ```ini
    [defaults]
    inventory = /root/ansible/inventory
    remote_user = root
    ask_pass = False
    roles_path = /root/ansible/roles/
    ```

    ```bash
    vim inventory
    ```
    Add the following content to `inventory`:
    ```ini
    [classroom]
    classroom
    ```

5. Create a role.
    ```bash
    mkdir roles
    ```

6. Copy the `classroom.zip` file and extract.
    ```bash
    pwd
    /root

    ls

    unzip classroom.zip

    cp -rav classroom/classroom /root/ansible/roles/
    cp classroom/classroom.yml /root/ansible/
    ```

7. Run the playbook `classroom.yml`.
    ```bash
    pwd
    /root/ansible

    ansible-playbook classroom.yml
    ```

**Note:** Make sure to adapt paths and commands based on your system configuration.



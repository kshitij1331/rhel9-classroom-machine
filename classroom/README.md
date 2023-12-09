

A simple classroom server setup based on real rhcsa exam server.
- ntp is configured
- httpd is configured
- nfs is configured

--------------------------before running the script----------------------------- 
- change the interface name in "./classroom/classroom/network/config.yml" file
- change the hosts in "./classroom/classroom.yml".


--------------------------how to run the script :--------------------------------
1. create a new rhel9  machine with yum locally configured on it with network adapters.
2. set hostname and domain name.
        # hostnamectl set-hostname classroom
        # vim /etc/hosts
                    172.25.250.254   content.example.com  classroom

2. install ansible 
    # yum install ansible -y
3. configure ansible
     # pwd
            /root
     # mkdir ansible
     # cd ansible
     # vim ansible.cfg
                    [defaults]
                    inventory = /root/ansible/inventory
                    remote_user = root
                    ask_pass = False
                    roles_path = /root/ansible/roles/
     # vim inventory
                    [classroom]
                    classroom
                    
4. create a role
     # mkdir roles
    
5. copy classroom.zip file and extract
     # pwd
            /root
     # ls
     # unzip classroom.zip
     # cp -rav classroom/classroom /root/ansible/roles/
     # cp classroom/classroom.yml  /root/ansible/
     
6. Run the playbook classroom.yml
     # pwd
            /root/ansible
     # ansible-playbook classroom.yml
     

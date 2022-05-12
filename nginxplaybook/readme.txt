how to install ansible on ubuntu docker 
apt-get -y install openssh-client
apt-get install nano
apt install software-properties-common
apt-add-repository ppa:ansible/ansible
apt update
apt install ansible

nano /etc/ansible/hosts

[servers]
sahilvaiosystem ansible_host=192.168.1.105 ansible_ssh_private_key_file=/var/www/pathtoprivatesshkey

[all:vars]
ansible_python_interpreter=/usr/bin/python3


ansible-inventory --list -y
ansible all -m ping -u root


ansible-playbook -u sahil nginx-install.yaml


#ansible-playbook --private-key=${SSH_KEY} -i targets -e "@deployment_vars.yaml" -e "useDatabase=anydatabase" -u any-automation-user main.yaml
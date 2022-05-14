Default Inventory Folder is /etc/ansible/hosts

Prerequisites : Ansible should be installed

Step 1: Create inventory (Inventory is a list of hosts to connect to) 

Edit /etc/ansible/hosts file
nano /etc/ansible/hosts

# append this at the end of /etc/ansible/hosts file
# change these values to your original server details which will be used by ansile to connect to servers
# Dont change first line "[node_exp]", its like a variable we will be using in playbook

[node_exp]
centos_1 ansible_ssh_host=10.10.10.13 ansible_ssh_private_key_file=/home/didiet/.ssh/id_rsa ansible_ssh_user=centos
ubuntu_1 ansible_ssh_host=10.10.10.14 ansible_ssh_private_key_file=/home/didiet/.ssh/id_rsa ansible_ssh_user=ubuntu

# if key files are not already setup on server then set them up using the following commands
# change file paths or server details accordingly


ssh-copy-id -i ~/.ssh/id_rsa.pub centos@10.10.10.13
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@10.10.10.14

# make sure you are able to ssh to all the servers mentioned in hosts files with the help of ssh key before moving ahead

Step 2: Test the connection 

# this comman will ping all the mentioned server in the hosts file
# you should receive a pong in return for every server


Step 3: Download the node extractor folder including all the files including (node_exporter.yml, and templates folder and its files)

ansible -m ping node_exp


// example command to run this playbook 

ansible-playbook -vvv node_exporter.yml — extra-vars=”host=node_exp”

after this go to http://<ip_address>:9100/metrics to verify if no errors

Step 4: Run ansible playbook 
# first dry run the ansible to check the syntex
ansible-playbook -vvv node_exporter.yml -e ”host=node_exp” --check

# after dry run is successfull follow below
# run this following command as it is. do not change anything unles you know what you are doing
ansible-playbook -vvv node_exporter.yml -e ”host=node_exp”
or
ansible-playbook -vvv node_exporter.yml --extra-vars ”host=node_exp”
or
ansible-playbook -vvv node_exporter.yml —extra-vars=”host=node_exp”

Step 5: Test the service http://<ip_address>:9100/metrics



Note: daemon_reload: enabled

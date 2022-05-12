# ansipleplaybooks
these are some sample and test ansible playbooks

sample ansible command with ssh key and host

ansible-playbook --private-key=${SSH_KEY} -i targets -e "@deployment_vars.yaml" -e "useDatabase=${useDatabase}" -u psuk-automation main.yaml

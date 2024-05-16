Assumptions
3x clean Ubuntu 24.04 servers with SSH installed

The sceme will be following:
server1 - Ansible
server2 - Prometeus+Loki+Graphana
server3 - services


Prepare Ansible server
  sudo apt-get update
  sudo apt-get upgrade
  sudo apt-get install ansible -y
  ansible --version

create keygen
  ssh-keygen

copy key from server1 to server2 and server3
ssh-copy-id "username"@"IP ADDRESS"

Configure passwordless sudo on server2 and server3
sudo visudo
username ALL=(ALL) NOPASSWD:ALL

Run Playbook to install DOcker on server2
ansible-playbook -i hosts.ini install_docker.yml

Run Playbook to install Prometeus+Loki+Graphana on server2
ansible-playbook -i hosts.ini deploy_monitoring_stack.yml

Run Playbook to setup Grafana Agent and exporters on server3
ansible-playbook -i hosts.ini install_grafana_agent_exporters.yml

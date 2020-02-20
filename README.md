### Ansible Demo

Use Of ansible in Azure cloud - [Official Documentation](https://docs.ansible.com/ansible/latest/scenario_guides/guide_azure.html)


PreReq Command to be execuated before run the paybooks are :

```
sudo apt-get update
sudo apt-get install python3-venv
sudo apt install python3-pip
pip3 install virtualenv
virtualenv -p python3 .venv
source .venv/bin/activate
pip3 install ansible
git clone https://github.com/samitkumarpatel/ansible-demo.git
cd ansible-demo/
---make the necessary change for ansible inventory---
sudo apt-get install sshpass
ansible-playbook -i inventories/cloud/host.yml install-docker.yml -e ansible_python_interpreter=python3

```


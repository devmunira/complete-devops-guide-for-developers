### Setup Web server using httpd with loadbalancer

#### Steps:

- Initialize an Ansible configuration file: `ansible-config init --disabled > ansible.cfg`
- `key.pem`: This file contains the private key for your target node.
- Secure your key.pem file: `chmod 400 key.pem`
- Create Inventory and Inventory Jinja file
- Create Aws Credentials and Instance Variable file
- Create Playbook for create aws ec2 instance

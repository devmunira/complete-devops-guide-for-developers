# Ansible

<!-- what is Ansible -->

Ansible is an open-source automation tool that simplifies IT automation, configuration management, application deployment, and orchestration. It uses a declarative language (YAML) to describe system configurations and can manage both Linux and Windows systems.

### Key characteristics:

- Agentless: No software needs to be installed on managed nodes
- Simple: Uses YAML syntax for playbooks
- Powerful: Can automate complex multi-tier IT application environments
- Secure: Uses SSH for secure connections
- Efficient: Parallel execution across multiple servers

<!-- What problems it solves -->

### Ansible solves several critical IT infrastructure challenges:

1. **Configuration Management**

   - Ensures consistent system configurations across multiple servers
   - Eliminates configuration drift
   - Provides version control for infrastructure changes

2. **Application Deployment**

   - Automates application deployment processes
   - Reduces deployment time and human errors
   - Enables blue-green deployments and rollbacks

3. **Infrastructure Provisioning**

   - Automates server provisioning and setup
   - Integrates with cloud providers (AWS, Azure, GCP)
   - Manages infrastructure as code

4. **Continuous Delivery**

   - Integrates with CI/CD pipelines
   - Automates testing and deployment workflows
   - Ensures consistent deployment across environments

5. **Security and Compliance**

   - Automates security patch management
   - Ensures compliance with security policies
   - Centralizes security configurations

6. **Disaster Recovery**
   - Automates backup and recovery procedures
   - Ensures consistent disaster recovery processes
   - Reduces recovery time objectives (RTO)

<!-- How Configure Ansible into AWS -->

### How Configure Ansible into AWS

- Initialize an Ansible configuration file: `ansible-config init --disabled > ansible.cfg`
- `key.pem`: This file contains the private key for your target node.
- Secure your key.pem file: `chmod 400 key.pem`
- Execute an Ansible ad-hoc command to display the current date on all hosts: `ansible all -m command -a "date"`
- Run an Ansible playbook: `ansible-playbook <playbook name>`
- Refer to the Jinja Template Documentation for more information: https://jinja.palletsprojects.com/en/3.0.x/templates/
- Explore the Ansible AWS Collection by visiting the following link: https://galaxy.ansible.com/ui/repo/published/community/aws/
- Ansible ec2-instance module documentation: https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_instance_module.html#ansible-collections-amazon-aws-ec2-instance-module
- My Ansible Role in Ansible-galaxy : https://github.com/Trainersudhanshu/AnsibleRole

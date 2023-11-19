# Install a test Zabbix environment wth Ansible

This setup will install 1 Zabbix server (with mysql, apache, php and zabbix-web) 
and install 2 Zabbix clients and will add these to the Zabbix server.

## Pre-requisites

- Ansible 2.10 or higher
- Python3 with virtualenv
- 3 VM's or Multipass instances
  - `zabbix-server`
  - `zabbix-client01`
  - `zabbix-client02`
- A user with `sudo` privileges on the VM's or Multipass instances 
  (defaults to the current user)

## Setup

### 1. Modify the `inventory` file

Change the IP addresses of the hosts to reflect your environment.

### 2. Install a Python virtual environment

Create a Python virtual environment and install all the required modules.

```shell
python3 -m venv ~/venv
source ~/venv/bin/activate
python3 -m pip install -r requirements.txt
```

### 3. Install the needed collections and roles

We depend on specific collections and roles which need to be installed. Because 
of the settings in `ansible.cfg` these will be installed in the respective 
`collections` and `roles` directory within this directory instead of the default 
location.

```shell
ansible-galaxy install -r requirements.yml
```

### 4. Run the playbook to install Zabbix

This playbook has 4 plays defined, which are documented within the playbook.

```shell
ansible-playbook playbooks/site.yml
```

In the end you can reach Zabbix on <http://[ip_of_zabbix_server]/zabbix> and use 
the default login details: `Admin/zabbix`

## Author

Chris van Meer - <chris.vanmeer@atcomputing.nl>

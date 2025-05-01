# Infra Deploy 3Host

This project is an **Ansible-based automation** for setting up a domain infrastructure on **three hosts**: one server and two client machines. The goal of this project is to automate the deployment of essential services such as **Samba (Domain Controller)**, **DNS**, **DHCP**, **Nginx**, and **Firewall** on a server. The client machines are then joined to the domain automatically.

## Project Overview

The infrastructure consists of the following components:

- **Server**: This machine hosts the domain controller, DNS, DHCP, Nginx web server, and firewall.
- **Client 1 and Client 2**: These machines are automatically joined to the domain created by the Samba Domain Controller.

The automation is achieved through **Ansible** playbooks that configure all the services on the server and clients, ensuring a seamless setup.

## Requirements

To run this project, you need:

- **Ubuntu 20.04** or compatible Linux-based systems
- **Ansible** installed on the management machine (the machine running Ansible)
- SSH access to all the machines in your infrastructure (server and clients)

## Installation

### 1. Clone the Repository

First, clone the repository to your local machine:

git clone https://github.com/devkans/infra-deploy-3host.git
cd infra-deploy-3host


###2. Configure Inventory File
The inventory file is where you define the server and client machines. It contains the IP addresses, usernames, and SSH key paths for connecting to the machines.

Here is an example of what the inventory file might look like:

ini
[server]
192.168.5.12 ansible_user=your_user ansible_ssh_private_key_file=path_to_ssh_key

[client1]
192.168.5.5 ansible_user=client1_user ansible_ssh_private_key_file=path_to_ssh_key

[client2]
192.168.5.6 ansible_user=client2_user ansible_ssh_private_key_file=path_to_ssh_key
Make sure to update the file with the correct details:

ansible_user: Replace this with the username for each machine (e.g., ubuntu or root).

ansible_ssh_private_key_file: Provide the path to the SSH private key you will use to connect to the machines.

IP addresses: Update the IPs to reflect the actual addresses of your server and clients.

3. Modify Ansible Playbook (if needed)
The playbooks are designed to set up the server and clients. You can adjust the settings in the playbook files, such as server IP addresses, domain names, etc.

You may also need to update the hosts in the playbooks to match your server and client names.

4. Run the Ansible Playbook
After setting up your inventory file and making any necessary adjustments to the playbooks, run the playbook on your management machine:

bash
ansible-playbook -i inventory server_playbook.yml
This will configure the server, set up all services, and ensure the clients are joined to the domain.

Services Configured
Samba (Domain Controller): Provides the Active Directory and Domain services.

DNS: DNS services are configured to support the Samba domain.

DHCP: The server will automatically assign IP addresses to clients within the network.

Nginx: A simple web server configured for the infrastructure.

Firewall: The server’s firewall is configured to allow necessary ports for Samba, DNS, and DHCP.

Directory Structure
graphql
infra-deploy-3host/
│
├── playbooks/
│   ├── server_playbook.yml        # Playbook for configuring the server
│   ├── client_playbook.yml        # Playbook for configuring the clients
│
├── templates/
│   ├── samba_config_template.conf # Template for Samba configuration
│   ├── dns_config_template.conf   # Template for DNS configuration
│   ├── dhcp_config_template.conf  # Template for DHCP configuration
│
├── inventory                      # Ansible inventory file with host details
└── README.md                      # This README file
Troubleshooting
SSH Access Issues: Ensure you have SSH access to the server and client machines. You can test SSH access with ssh username@ip_address.

Firewall Issues: Make sure that the required ports are open on the server and clients. You may need to adjust firewall settings based on your environment.

Permissions Issues: Ensure that the Ansible user has the necessary permissions to execute tasks on the server and clients. You might need to use sudo for elevated privileges.

License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgments
Thanks to Ansible for making infrastructure automation simple.

Thanks to Samba for the free software to implement Active Directory.

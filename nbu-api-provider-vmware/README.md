nbu-api-provider-vmware
=======================

# Description

A sample Ansible role for adding a VMware vCenter server to NetBackup using the API

# Requirements

This role has the following requirements:

  - Ansible 2.9+
  - NetBackup 9.0+
  - Linux Based Master Server ("See note 1")
  - SSH keyless access between Ansible host and the NetBackup servers
  - API Key for Administrative NetBackup user

Notes:

  1. All tasks utilize the Ansible URI module - This module is developed for Unix based systems. For Windows based master servers, utilize the WIN_URI module instead. 

# Assumptions

To utilize this role, in-depth knowledge of both Veritas NetBackup and Ansible is required

# How to use the role

This role is part of a collection of roles available in netbackup-ansible project. To use the role:

  1. Clone the repository from GitHub and move to your Ansible Control Host:

           git clone http://www.GitHub/ansible/netbackup-ansible.git

  2. Update the role variables: 

           - playbook

               NBU_MASTER_SERVER - Hostname of the NetBackup Master Server
               NBU_API_KEY - User's API key for authenticating with NetBackup API

           - default/main.yml

               limit_vcenter -  Maximum streams on vCenter server
               limit_datastore: Maximum streams on datastore
               limit_esxserver: Maximum streams on ESX Server
               nbu_vmware_server: <Hostname or IP Address>
               nbu_vmware_type: VMWARE_VIRTUAL_CENTER_SERVER
               nbu_vmware_username: <Username for vCenter> (*)
               nbu_vmware_password: <Password for vCenter User> (*)

           (*) Its recommended to migrate these secrets into an encrypted vars file or to a secrets management platform

  3. Create a playbook and Inventory file

            Examples are provided below in the next section

  4. Provide an inventory and execute the playbook on the master server or Linux server with access HTTPS access to the NetBackup master server:

           "ansible-playbook <playbook_name> -i <inventory_file> "

# Example Playbook / Inventory

A sample playbook and invetory file is provided below:

  1. Example "playbook.yml" file

           - name: Veritas -> Add credentials to NetBackup for VMware
             hosts: master
             gather_facts: no
             roles:
               - nbu-api-provider-vmware
             vars:    
                NBU_MASTER_SERVER: <Hostname_master_server>
                NBU_API_KEY: <API-KEY>
             tags:
               - add_vcenter_server

  2. Example "inventory.yml" file

	        [localhost]
	        locahost ansible_host=localhost

	        [master]
	        <fqdn1> ansible_host=<ip_address>

# Version

| Directory Name | Version | Description | 
| :--- | :--- |:--- |
| nbu-api-provider-vmware | 1.0 | Inital release |

# License

The following components are available under the General Public License �GPL� 2.0 and/or the General Public License �GPL 3.0� provided herein. The source code for these GPL component(s) may be obtained at: https://github.com/VeritasOS/netbackup-ansible




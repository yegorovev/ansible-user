Role Name
=========

Provisioning linux user for ansible roles.

Requirements
------------

Inventory: Rocky Linux release 8.6 (Green Obsidian)
Python 3.8.10

Role Variables
--------------

- user_name: provisioner
- temporal_ssh_key: /tmp/id_ssh_rsa

Dependencies
------------
See requirements.txt

Example Playbook
----------------
groups_vars/all.yml

	user_name: provisioner
	temporal_ssh_folder: "{{ lookup('env', 'PWD') }}"
	temporal_ssh_key: "{{ temporal_ssh_folder }}/id_{{ user_name }}_rsa"

role.yml

	- hosts: localhost
	  connection: local
	  gather_facts: false
	  become: no
	  tasks:
		- name: Generate ssh keys
		  openssh_keypair:
			path: "{{ temporal_ssh_key }}"
			size: 4096
			type: rsa

	- hosts: all
	  tasks:
		- name: Provisioning Ansible user
		  import_role:
			name: ansible_user


Author Information
------------------
#

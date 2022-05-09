.. title: Ansible
.. slug: ansible
.. date: 2022-05-09 19:30
.. tags:
.. category: misc:ansible
.. link:
.. description:
.. type: text
.. priority: 1
.. author: Nils Tonnätt

`Ansible <https://www.ansible.com/>`_ is a tool for managing a fleet of machines.
There might be some tasks that you have to execute on every machine in your data center.

---

Playbooks
=========

Instead of logging in in every machine via SSH, we write an Ansible playbook
that describes all tasks in a YAML file.

 .. code-block:: yaml

	---
	- name: Installing packages
	  hosts: web
	  become: yes
	  gather_facts: no
	  tasks:
	    - name: Install git
	      apt:
		  name: git
		  state: present
		  update_cache: yes
	    - name: Install ALSA
	      apt:
		  name: alsa
		  state: present
		  update_cache: yes
	    - name: Install ALSA Dev
	      apt:
		  name: libasound2-dev
		  state: present
		  update_cache: yes
	    - name: Install Jack
	      apt:
		  name: jackd2
		  state: latest
		  update_cache: yes

By default Ansible logs into every machine via SSH. `hosts: web` tells ansible
to execute following tasks on all machines in the inventory group web.
Installing packages with APT requires superuser permissions. `become: yes` tells
Ansible to become root. The default method for this is sudo.

The biggest benefit over shell scripts is that it is possible to describe the
state of a machine. In the example four packages will be installed.
Only jackd2 will be updated if it is already present.

---

Inventory
=========

For executing our new playbook Ansible needs to know what machines are in our
inventory. The inventory can be written in INI or YAML syntax.

 .. code-block:: ini
	[local]
	localhost

	[web]
	google.de
	facebook.de

The default location for your inventory file is `/etc/ansible/hosts`.

For more information for creating your inventory see the official
`user guide <https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html>`_.

---

ansible.cfg
===========

A separate inventory file can be set for your project in an Ansible configuration
file `ansible.cfg`:

 .. code-block:: ini
	[defaults]
	inventory = hosts
	ansible_ssh_user = studio
	sudo_user = studio

This file sets the location of your inventory file to `./hosts`. Furthermore
the default SSH user as well as the sudo user gets set to `studio`.

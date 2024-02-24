# Ansible role: labocbz.install_unattended_upgrades

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Cbz-blue)

## Description

![Tag: Unattended-upgrades](https://img.shields.io/badge/Tech-Unattended--upgrades-orange)

An Ansible role to install an configure Unattended-upgrades on your host.


The Ansible role for unattended upgrades installation automates the process of keeping your system up to date by applying critical and security updates without requiring manual intervention. This role utilizes a few variables to customize its behavior.

By default, automatic reboot after updates is disabled, as indicated by the "install_unattended_upgrades__automatic_reboot" variable set to "false". This means that the system will not automatically restart after installing updates.

If you want to enable automatic reboot, you can change the value of the "install_unattended_upgrades__automatic_reboot" variable to "true". However, be aware of the potential implications of automatic reboot in your environment.

Additionally, if you choose to enable automatic reboot, you can specify the time at which the reboot should occur using the "install_unattended_upgrades__automatic_reboot_time" variable. In this example, the time is set to "06:00", indicating that the system will automatically restart at 6 AM.

To receive reports on the updates performed by the role, you can provide an email address in the "install_unattended_upgrades__report_email_address" variable. In this example, the configured email address is "your.address@domain.tld". You will receive email notifications containing information about the applied updates.

By using this Ansible role for unattended upgrades installation, you can easily keep your system up to date and secure by automating the update process and customizing its behavior according to your requirements.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
install_unattended_upgrades__automatic_reboot: false
install_unattended_upgrades__automatic_reboot_time: "06:00"

install_unattended_upgrades__report_email_address: "your.address@domain.tld"

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
inv_install_unattended_upgrades__automatic_reboot: false
inv_install_unattended_upgrades__automatic_reboot_time: "06:00"

inv_install_unattended_upgrades__report_email_address: "my.address@domain.tld"

```

```YAML
# From AWX / Tower
---

```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.install_unattended_upgrades"
  tags:
    - "labocbz.install_unattended_upgrades"
  vars:
    install_unattended_upgrades__automatic_reboot: "{{ inv_install_unattended_upgrades__automatic_reboot }}"
    install_unattended_upgrades__automatic_reboot_time: "{{ inv_install_unattended_upgrades__automatic_reboot_time }}"
    install_unattended_upgrades__report_email_address: "{{ inv_install_unattended_upgrades__report_email_address }}"
  ansible.builtin.include_role:
    name: "labocbz.install_unattended_upgrades"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-04-27: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez

### 2023-10-06: New CICD, new Images

* New CI/CD scenario name
* Molecule now use remote Docker image by Lord Robin Crombez
* Molecule now use custom Docker image in CI/CD by env vars
* New CICD with needs and optimization

### 2024-02-24: Fix and CI

* Added support for new CI base
* Edit all vars with __

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)

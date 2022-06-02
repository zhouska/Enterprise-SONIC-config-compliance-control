# Enterprise-SONIC-config-compliance-control
# Description

Imagine you have some blacklisted/forbidden vlans/interfaces which users cannot configure on the switch. This project offers a simple solution to this problem using jinja2 and ansible.

# Intended functionality
- ensure the forbidden vlans/interfaces cannot be configured by the user
- save switch config on the switch and export a copy into local directory ``backups``
- tested on: ansible 2.10-2.12, Enterprise SONIC 4.0 and [Enterprise SONIC ansible collections](https://github.com/ansible-collections/dellemc.enterprise_sonic) version 1.1.0
- caveats: range of consecutive vlans will cause the playbook to fail (to be solved in upcoming Enterprise SONIC ansible collection versio 2.0)

# How to use this project:
- edit list of target hosts in ``inventory``
- create ``ansible.cfg`` to suit your needs
- edit list of forbidden and allowed vlans/interfaces to your liking. Don't forget it needs to be use python dictionary structure because of used function pop().
- run the ansible playbook generate_files.yaml: ``ansible-playbook generate_files.yaml``. It will create/update ansible playbook ``compliance_check_and_config.yaml`` using the input files from previous step.
- run the ansible playbook main.yaml: ``ansible-playbook main.yaml`` to configure the switches

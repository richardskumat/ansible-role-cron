ansible-role-cron
=========

This is a personal fork of https://github.com/weareinteractive/ansible-cron.

This is a role that

- installs cron
- adds cron tasks
- configures service

Requirements
------------

Ansible > 2.8

Role Variables
--------------

Here is a list of all the default variables for this role, which are also available in defaults/main.yml.

---
# cron_tasks:
#   - name: ...
#     cron_file: ...
#     day: ...
#     hour: ...
#     job: ...
#     minute: ...
#     month: ...
#     special_time: ...
#     state: ...
#     user: ...
#     weekday: ...
#

# list of cron entries (@see http://docs.ansible.com/cron_module.html)
cron_tasks: []
# start on boot
cron_service_enabled: yes
# current state: started, stopped
cron_service_state: started
#
# refer to the `cronvar Ansible module documentation <https://docs.ansible.com/ansible/cronvar_module.html>`_ for details.
#
# cron_vars:
#   - name: 'PATH'
#     value: '/usr/bin:/bin:/usr/local/bin'
#     user: 'root'
#
cron_vars: []

Handlers

These are the handlers that are defined in handlers/main.yml.

---
# For more information about handlers see:
# http://www.ansibleworks.com/docs/playbooks.html#handlers-running-operations-on-change
#

- name: restart cron
  service:
    name: "{{ cron_service_name }}"
    state: restarted
  when: cron_service_state != 'stopped'


Dependencies
------------

N/A

Example Playbook
----------------

---

- hosts: all
  roles:
    - richardskumat.ansible_role_cron
  vars:
    cron_tasks:
      - name: checking dirs
        special_time: daily
        job: "ls -alh > /dev/null"

License
-------

MIT

Author Information
------------------

We Are Interactive original@2019

Link: https://github.com/weareinteractive

Richard Skumat fork@2019

Link: https://github.com/richardskumat/ansible-role-cron

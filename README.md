[![CI](https://github.com/de-it-krachten/ansible-role-olam/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-olam/actions?query=workflow%3ACI)


# ansible-role-olam

Installs Oracle Linux Automation Manager (OLAM), Oracle's implementation of AWX<br>
This role is based on https://docs.oracle.com/en/learn/olam-install<br>


Platforms
--------------

Supported platforms

- OracleLinux 8



Role Variables
--------------
<pre><code>
# Should IPv6 be disabled in nginx
olam_disable_ipv6: false

# Use self-signed certificates
olam_ssc: true

# Location where to write installation logs
olam_log_dir: /var/lib/ol-automation-manager

# IP address used for OLAM
olam_service_ip: "{{ ansible_all_ipv4_addresses[0] }}"

# OLAM admin user
olam_admin_username: admin
olam_admin_email: admin@example.com

# List of awx-manage commands to run
olam_awx_manage_cmds:
  - command: awx-manage migrate
    log: awx-manage-migrate.log
  - command: awx-manage createsuperuser --username {{ olam_admin_username }} --email {{ olam_admin_email }} --noinput
    log: awx-manage-createsuperuser.log
  - command: awx-manage create_preload_data
    log: awx-manage-create_preload_data.log
  - command: awx-manage provision_instance --hostname={{ olam_service_ip }}
    log: awx-manage-provision_instance.log
  - command: awx-manage register_queue --queuename=tower --hostnames={{ olam_service_ip }}
    log: awx-manage-register_queue.log

# key/value pairs to put in /etc/tower/settings.py
olam_settings:
  CLUSTER_HOST_ID: "{{ olam_service_ip }}"
</pre></code>


Example Playbook
----------------

<pre><code>
- name: Converge
  hosts: all
  vars:
  tasks:
    - name: Include role 'ansible-role-olam'
      include_role:
        name: ansible-role-olam
</pre></code>

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
olam_admin_password: admin
olam_admin_email: admin@example.com

# Should demo data be loaded
olam_demo_data: true

# key/value pairs to put in /etc/tower/settings.py
olam_settings:
  CLUSTER_HOST_ID: "{{ olam_service_ip }}"
</pre></code>


Example Playbook
----------------

<pre><code>
- name: sample playbook for role 'olam'
  hosts: all
  vars:
  tasks:
    - name: Include role 'olam'
      include_role:
        name: olam
</pre></code>

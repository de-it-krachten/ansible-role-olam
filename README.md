[![CI](https://github.com/de-it-krachten/ansible-role-olam/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-olam/actions?query=workflow%3ACI)


# ansible-role-olam

Installs Oracle Linux Automation Manager (OLAM), Oracle's implementation of AWX<br>
This role is based on https://docs.oracle.com/en/learn/olam-install<br>



## Dependencies

#### Roles
- deitkrachten.openssl

#### Collections
- community.general
- ansible.posix
- community.postgresql

## Platforms

Supported platforms

- OracleLinux 8

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# OLAM version
olam_version: 1

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

# Expose postgresql database externally
olam_db_external: false

# database name, username and password
olam_db_name: awx
olam_db_user: awx
olam_db_password: awx
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'olam'
  hosts: all
  become: "yes"
  vars:
    olam_db_external: True
    olam_disable_ipv6: True
  tasks:
    - name: Include role 'olam'
      ansible.builtin.include_role:
        name: olam
</pre></code>

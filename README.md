[![CI](https://github.com/de-it-krachten/ansible-role-olam/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-olam/actions?query=workflow%3ACI)


# ansible-role-olam

Installs Oracle Linux Automation Manager (OLAM), Oracle's implementation of AWX
This role is based on https://docs.oracle.com/en/learn/olam-install


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

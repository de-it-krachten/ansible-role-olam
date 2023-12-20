[![CI](https://github.com/de-it-krachten/ansible-role-olam/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-olam/actions?query=workflow%3ACI)


# ansible-role-olam

Installs Oracle Linux Automation Manager (OLAM), Oracle's implementation of AWX<br>
This role is based on https://docs.oracle.com/en/learn/olam-install<br>



## Dependencies

#### Roles
- deitkrachten.firewalld
- deitkrachten.firewall
- deitkrachten.openssl
- deitkrachten.postgresql
- deitkrachten.python
- deitkrachten.redis

#### Collections
- containers.podman
- community.general
- containers.podman

## Platforms

Supported platforms

- OracleLinux 8

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# OLAM version
olam_version: 2

# Should IPv6 be disabled in nginx
olam_disable_ipv6: false

# Postgresql settings
olam_postgresql_version: 13
olam_db_name: awx
olam_db_host: localhost
olam_db_port: 5432
olam_db_user: awx
olam_db_password: awx

# Location where to write installation logs
olam_log_dir: /var/lib/ol-automation-manager

# IP address used for OLAM
olam_service_ip: "{{ ansible_all_ipv4_addresses[0] }}"

# OLAM admin user
olam_admin_username: admin
olam_admin_password: admin
olam_admin_email: admin@example.com

# Define content of /etc/tower/SECRET_KEY
# olam_secret_key: my-very-secret-key

# Should demo data be loaded
olam_demo_data: true
#olam_demo_data: false

# # Expose postgresql database externally
# olam_db_external: false

# OLAM hostname
olam_hostname: "{{ ansible_hostname }}"

# awxkit (awx/olam cli)
olam_install_awxkit: true

# List of pypi packages to install
olam_awxkit_packages:
  - "awxkit==19.4.0"

# venv root
olam_awxkit_venv_path: /usr/local/venv/awxkit

# Python version to use
olam_awxkit_venv_python: /usr/bin/python3.9
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'olam'
  hosts: all
  become: 'yes'
  vars:
    olam_db_external: true
    olam_disable_ipv6: true
    ansible_python_interpreter: /usr/bin/python3
    firewall_ports:
      - port: 80
        proto: tcp
      - port: 443
        proto: tcp
    postgresql_version: 13
    postgresql_db_name: awx
    postgresql_db_user: awx
    postgresql_db_password: awx
    postgresql_password_encryption_scheme: scram-sha-256
    postgresql_install_optional_packages: true
    redis_settings:
      maxmemory: 100mb
      maxmemory-policy: volatile-ttl
      bind: 127.0.0.1
      supervised: systemd
      unixsocket: /var/run/redis/redis.sock
      unixsocketperm: '775'
    olam_ssl_remote_src: true
    olam_ssl_key: /etc/pki/tls/private/{{ inventory_hostname }}.key
    olam_ssl_certificate: /etc/pki/tls/certs/{{ inventory_hostname }}.crt
  roles:
    - deitkrachten.python
    - deitkrachten.firewalld
    - deitkrachten.firewall
    - deitkrachten.postgresql
    - deitkrachten.redis
    - deitkrachten.openssl
    - deitkrachten.redis
  tasks:
    - name: Include role 'olam'
      ansible.builtin.include_role:
        name: olam
</pre></code>

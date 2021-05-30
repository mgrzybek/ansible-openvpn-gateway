ansible-openvpn-gateway
=======================
Ansible role to deploy an OpenVPN gateway on BSD systems.

Requirements
------------

When used within a jail, [some configuration is
needed](https://www.carlomaiorano.me/freebsd/2019/02/18/openvpn-freebsd-jail.html)

Role Variables
--------------

``` yaml
openvpn_gateway_internal_iface: the network device to use for trafic forwarding
openvpn_gateway_connection:
  name: connection name (used by monitoring)
  auth:
    login: myself
    password: secret
  servers:
  - server: hostname
    port: port number
    protocol: tcp or udp
  certificate: |
    -----BEGIN CERTIFICATE-----
    data
    -----END CERTIFICATE-----
  tls_auth: |
    -----BEGIN OpenVPN Static key V1-----
    data
    -----END OpenVPN Static key V1-----
```

Dependencies
------------

N.A.

Example Playbook
----------------

``` yaml
- hosts: servers
  roles:
  - role: ansible-openvpn-gateway
  vars:
    openvpn_gateway_internal_iface: re0
    openvpn_gateway_connection:
      name: my-private-service
      auth:
        login: myself
        password: secret
      servers:
      - server: vpn1.example.org
        port: 443
        protocol: tcp
      - server: vpn2.example.org
        port: 1194
        protocol: udp
      certificate: |
        -----BEGIN CERTIFICATE-----
        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
        fk7xbAU8oH9AJvx7BKyMc419sCI5kdpn0Q==
        -----END CERTIFICATE-----
```

Testing
-------

This role provides a `Vagrantfile` and a `Makefile`.

``` bash
# Makefile-provided commands
$ make help
help                This help message
lint                Test YAML syntax
vagrant-destroy     Destroy vagrant boxes
vagrant-variables   Test vagrant env variables
vagrant-vbox        Test the playbook using vagrant and virtualbox
# Optionnal variables
$ export VAGRANT_BOX_NAME="my-box"
$ export VAGRANT_BOX_URL="http://repo/my-box.box"
$ export VAGRANT_VM_CPUS=1
$ export VAGRANT_VM_MEMORY=1024
# Vagrant using Virtualbox
$ make vagrant-vbox
$ make vagrant-destroy
```

License
-------

GPL-3+

Author Information
------------------

Mathieu GRZYBEK

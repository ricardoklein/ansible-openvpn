[![Build Status](https://travis-ci.org/ricardoklein/.png)](https://travis-ci.org/ricardoklein/)

# ricardoklein.openvpn

Install and setup openvpn into opensuse Leap
This role also manages the users, you can list the enabled and revoked users
and the role is going to create or revoke any user that you add/move in the
variables. It also generates the user.ovpn inside `/etc/openvpn/clients` so
you can easily distribute them.

Currently supports:

* OpenSuse Leap 15.2

## Requirements

No extra requirements needed.

## Role Variables

This is an example of how to setup your variables

```yaml
# VPN
openvpn_key_country: DE
openvpn_key_province: BR
openvpn_key_city: Nuremberg
openvpn_key_org: RKleinORG
openvpn_key_email: rklein@domain.com
openvpn_key_size: 4096

# OPENVPN Clients
# Create hashed password with:
#   PASSWORD=$(pwgen -n 20 -1) && echo "PASSWORD TEXT: ${PASSWORD}" && \
#   echo "PASSWORD HASH: $(openssl passwd -salt CHOOSEYOURSALT -1 ${PASSWORD})"

ansible_openvpn__clients:
  - { name: "user1", password: "$1$SALT$foobarpassowrdautomaticgenerated" }
  - { name: "user2", password: "$1$SALT$foobarpassowrdautomaticgenerated" }

ansible_openvpn__clients_revoked:
  - { name: "revokeduser1" }

```

## Dependencies

No deps.

## Example Playbook

```
    - hosts: servers
      roles:
         - { role: ricardoklein.openvpn }
```

## License

GPL

## Author Information

If you want to suggest changes or request new features,
please feel free to create a issue or send a pull request.

## ToDo

* Add support for ipv6
* Download the .ovpn files if user want

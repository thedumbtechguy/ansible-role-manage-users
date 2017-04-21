# Ansible Role: Manage Users

An ansible role to manage users on linux hosts.

## Requirements

Requires a custom `authorized_keys` location (`/etc/ssh/authorized_keys/`) to be setup.
You can configure this using the Todo: link to server_setup role.

> This role has been tested on `Ubuntu 16.04` and `Ubuntu 16.10` only.

## Variables

- `users`: list of users to create.
  - Default: `[]`
  - Example
    ```yaml
    users:
      - username: *username
        password: *"someencryptedvalue"
        use_ssh: false
        public_key: private key string or url
        use_sudo: false
        sudo:
          hosts: ALL
          groups: ALL
          users: ALL
          commands: ALL
    ```
    > **Note**: Password should be an encrypted value compatible with the [ansible user module](http://docs.ansible.com/ansible/user_module.html).


## Usage Example

```yaml
- hosts: all
  vars:
    users:
      - username: admin
        password: '$1$ThisIsSo$RwIOJHdSWIzAJjbvBdbOZ0'
        use_sudo: true
        use_ssh: false
      - username: ansible
        password: '$1$ThisIsSo$RwIOJHdSWIzAJjbvBdbOZ0'
        use_ssh: true
        public_key: 'ssh-rsa AAAA......'
        use_sudo: true
        sudo:
          hosts: ALL
          groups: ALL
          users: ALL
          commands: ALL
  roles:
    - thedumbtechguy.manage-users
```


## License

MIT / BSD

## Author Information

This role was created by [Stefan Froelich](https://thedumbtechguy.blogspot.com/).

## Credits
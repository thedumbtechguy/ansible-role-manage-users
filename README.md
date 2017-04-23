# Ansible Role: Manage Users

An ansible role to manage users on linux hosts.

## Requirements

Requires a custom `authorized_keys` location (`/etc/ssh/authorized_keys/`) to be setup.

You can configure this using the [thedumbtechguy.server-setup](https://galaxy.ansible.com/thedumbtechguy/server-setup/) role.

> This role has been tested on `Ubuntu 16.04` and `Ubuntu 16.10` only.

## Variables

- `users`: list of users to create.
  - Default: `[]`
  - Example
    ```yaml
    users:
      - username: username # required
        password: 'encryptedpassword' # optional. omitted if not provided
        use_ssh: false # optional. defaults to false
        public_key: 'key url or contents' # required when 'use_ssh' is true
        use_sudo: false # optional. defaults to false
        sudo:
          hosts: ALL # optional. defaults to 'ALL'
          groups: ALL # optional. defaults to 'ALL'
          users: ALL # optional. defaults to 'ALL'
          commands: ALL # optional. defaults to 'ALL'. for passwordless sudo, use 'NOPASSWD: ALL'
    ```
    > **Note**: Password should be an encrypted value compatible with the [ansible user module](http://docs.ansible.com/ansible/user_module.html).
    >
    >  You can create one using: `python -c 'import crypt; print crypt.crypt("This is the password", "$1$ThisIsSomeSalt$")'`


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

This role was created by [TheDumbTechGuy](https://github.com/thedumbtechguy) ( [twitter](https://twitter.com/frostymarvelous) | [blog](https://thedumbtechguy.blogspot.com) | [galaxy](https://galaxy.ansible.com/thedumbtechguy/) )

## Credits
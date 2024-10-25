# ERPNext Podman Ansible role

An Ansible role for installing and configuring ERPNext as a systemd service
using rootless Podman containers in Rocky Linux 9, though likely supporting
older versions and other OSes.

## Usage

If so desired, change the default values for `erpnext_mysql_user_pw` and
`erpnext_mysql_root_pw` (both are set to `admin` by default).

```yaml
- name: Podman configuration
  hosts: all
  # vars:
  #   erpnext_mysql_user_pw: admin
  #   erpnext_mysql_root_pw: admin
  roles:
    - erpnext-podman-ansible-role
```

## License

MIT

## Author Information

Randy Eckman (Stretch Your Mind Entertainment LLC)

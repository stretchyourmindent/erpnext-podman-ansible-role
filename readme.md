# ERPNext Podman Ansible role

An Ansible role for installing and configuring ERPNext as a systemd service
using rootless Podman containers in Rocky Linux 9, though likely supporting
older versions and other OSes.

## Usage

Set the variables `erpnext_base_url` and `erpnext_host` accordingly.

If so desired, change the default values for `erpnext_mysql_root_pw`
(set to `admin` by default).
You may also consider updating the `erpnext_image`.

If you have additional Frappe apps you wish to install in your site in addition
to ERPNext, if they are included in your designated image, you can set
`erpnext_newsite_extra_args` to those command line flags.
For example: `erpnext_newsite_extra_args: --install-app taxjar_integration`

```yaml
- name: Podman configuration
  hosts: all
  vars:
    erpnext_base_url: https://erpnext.example.com
    erpnext_host: erpnext.example.com
    # erpnext_newsite_extra_args:
    # erpnext_image: docker.io/frappe/erpnext:latest
    # erpnext_mysql_root_pw: admin
  roles:
    - erpnext-podman-ansible-role
```

## SSH Keys

This role performs tasks that call `podman`, which, if done with a sudo user,
can cause Podman system misconfiguration for rootless containers running as
that user.  It is recommended to only perform tasks that call `podman` directly
as the user who will run the rootless container by using the `remote_user`
keyword.  This requires a new SSH connection as the given user, but will attempt
to use the default private key of the current Ansible invocation.  Therefore,
it is important to ensure that the ansible user's public key is also in the
`authorized_keys` file for the Podman user that will run the container.

## License

MIT

## Author Information

Randy Eckman (Stretch Your Mind Entertainment LLC)

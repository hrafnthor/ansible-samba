# ansible-samba
An Ansible role for setting up and configuring Samba shares

## Requirements / Dependencies

This role is dependent on `ansible.utils.jsonschema`.

## Setup

Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a requirements.yml file in the root directory of the playbook being worked on.

2. Add the following definition inside the requirements.yml file:

    ```yaml
    - name: hth-samba
      src: https://github.com/hrafnthor/ansible-samba.git
      scm: git
    ```

3. Install the requirements by executing

```cli
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role `hth-samba`.

### Scheme

```yaml

samba:
  users:                            [optional] List of users and the Samba password to set for them on the host
    - name: [string]                [required] The name of the user to configure
      password_var: [string]        [required] The Ansible variable name holding the password for the user
  shares:                           [optional] A list of shares to create on the host system
    - label: [string]               [required] The name of the samba share config file. If this changes then a new Samba share config file gets created.
      path: [string]                [required] The path to the share on the host
      comment: [string]             [optional] Comment that will accompany the share 
      browsable: [boolean]          [optional] Sets the share as browsable. Defaults to 'no'.
      writable: [boolean]           [optional] Sets the share as writable. Defaults to 'no'.
      read_only: [boolean]          [optional] Sets the share as read only. Defaults to 'no'.
      quests: [boolean]             [optional] Sets the share available to guest accounts. Defaults to 'no'.
      users: [string array]         [optional] Sets a list of allowed users and groups.
```

See official [Samba documentation](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html) here for detail information on each configuration option.

```yaml
samba:
  users:
    - name: john
      password_var: john_samba_password
  shares:
    - label: media
      path: "/home/john/public/media"
      comment: "This is John's media share"
      browsable: true
      writable: true
      read_only: false
      quests: false
      users:
        - steve
        - managers_group
```

## License

Apache License 2.0. See attached license file.

## Author Information

Hrafn Thorvaldsson. http://www.hth.is

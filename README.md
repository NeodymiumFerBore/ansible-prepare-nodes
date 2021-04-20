# ansible-prepare-nodes

Playbook that will prepare remote nodes to be managed with Ansible

---

## Description

- Create a user (dedicated to Ansible remote management)
- No password set: cannot connect except with an ssh key
- Add this user to sudoers file, NOPASSWD!!
- Add public ssh key to its authorized_keys file

---

## Usage

Change `devops_user` and `devops_public_key` variables in `group_vars/all` to fit your environment.

Then execute the playbook (warning: the affected nodes will reboot!)

Prepend the command with `ANSIBLE_HOST_KEY_CHECKING=False` if it's the first time your are connecting to the target(s)

```
$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory -u sudoeruser --tags reboot --ask-pass --become --ask-become-pass prepare-nodes.yml
```

Test your node(s) (they will not reboot):

```
$ ansible-playbook -i inventory -u devops_user prepare-nodes.yml
```


## Ansible Role Debugging

This repo contains sample code to help reproduce the Ansible issue reported here: https://github.com/ansible/ansible/issues/14017

### Setup

1. Clone the repo

2. Run `vagrant up` to start the test VM.

### Testing

To run the working example:

`ansible-playbook -i inventory playbook_working.yml`

To run the broken example:

`ansible-playbook -i inventory playbook_broken.yml`

In the working playbook, the `user` role is being included multiple times in the `role:` section.

In the broken playbook, the `user` role is being included multiple times via a wrapper role's dependencies.

### Notes

It seems that no matter which order the users are defined in, the instances where the `user_shell` variable is ommitted do not read the default from `./roles/user/defaults/main.yml`, but instead are set to whatever value was used in the last instance which did specify it.

# User

This is a parameterised role for creating one or more user accounts, and managing their SSH keys.

## Role Variables

| Var | Description | Required? |
| --- | ----------- | --------- |
| `user_username` | Username for the account                                                                                                                                            | Yes |
| `user_fullname` | The full name or comment for this account                                                                                                                           | Yes |
| | |
| `user_uid`      | If specified, the user's UID will be set to this integer, otherwise the UID is automatically generated.                                                             | No, defaults to automatic |
| `user_state`    | Whether the user should be `present` or `absent`. Note: When set to `absent`, the user's home folder (and all contents) **will be deleted**.                        | No defaults to `present` |
| `user_sudoers`  | A boolean used to control whether the user will have `sudo` rights or not. When set to `true`, the user will be able to use `sudo` without entering their password. | No defaults to `false` |
| `user_groups`   | An optional list of groups to add the account to (these are in addition to a default group with the same name as the account)                                       | No defaults to `[]` |
| `user_keys`     | An optional list of one or more SSH keys which will be added to `/<user_home>/.ssh/authorized_keys`                                                                 | No defaults to `[]` |
| `user_shell`    | An optional default shell for this user                                                                                                                             | No defaults to `/bin/bash` |
| `user_home`     | Optionally set a custom home folder for this user.                                                                                                                  | No defaults to `/home/<user_username>` |

## Example Playbook

Create a user with two SSH keys, and give them sudo rights:

```
---
- hosts: all
  roles:
    - role:          user
      user_state:    present
      user_username: ryan
      user_fullname: Ryan Conway
      user_sudoers:  true
      user_keys:
        - "ssh-rsa blablablablablablablablablablablablablablablablablablablabla key1@comment"
        - "ssh-rsa yadayadayadayadayadayadayadayadayadayadayadayadayadayadayada key2@comment"
```

Simply repeat to create as many user accounts as necessary:

```
---
- hosts: all
  roles:
    - role:          user
      user_state:    present
      user_username: ryan
      user_fullname: Ryan Conway
      user_sudoers:  true
      user_keys:
        - "ssh-rsa blablablablablablablablablablablablablablablablablablablabla key1@comment"
        - "ssh-rsa yadayadayadayadayadayadayadayadayadayadayadayadayadayadayada key2@comment"

    - role:          user
      user_state:    present
      user_username: someone
      user_fullname: Someone Else
      user_sudoers:  true
      user_keys:
        - "ssh-rsa etcetcetcetcetcetcetcetcetcetcetcetcetcetcetcetcetcetcetcetc key@comment"
```

To remove an account named `barney`:

```
---
- hosts: all
  roles:
    - role:          user
      user_state:    absent
      user_username: barney
```
   
You can also use this role as a dependency in another role, whilst still passing in the required parameters. This is useful to create 'wrapper' roles, which make it easy to refer to multiple users.

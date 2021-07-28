# shellScripts
Useful scripts I use

### ssh-update-id
Allows to update private key in remote ssh servers.

Its purpose is to facilitate the change of certificate in an environment where the access is done without requiring a password for each login.

Use a command like the following to renew the SSH key:
`$ ssh-update-id -i ~/.ssh/mykey -o ~/.ssh/oldkey  user@host`


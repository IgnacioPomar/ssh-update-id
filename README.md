# ssh-update-id
Allows to update private key in remote ssh servers.

Its purpose is to facilitate the change - reemplace an old pub key with a new one -, of the certificate in an environment where the access is done without requiring a password for each login.

That means, it will add first the new Pub key, and then using the new certificate, will conect an delete the old Pub key.



Use a command like the following to renew the SSH key (using the privat ekey of both certificates):

`$ ssh-update-id -i ~/.ssh/mykey -o ~/.ssh/oldkey  user@host`


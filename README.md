# ssh-update-id

**Easily rotate SSH keys on remote servers without losing access.**

`ssh-update-id` is a simple Bash utility designed to **replace an existing SSH key with a new one** on one or multiple remote hosts — without ever locking you out.

It’s ideal for environments where **passwordless SSH access** is used (e.g., using private/public key authentication), and you need to **update or rotate credentials** securely and seamlessly.

---

## 🔧 What it does

1. Connects to the remote host(s) using the **old private key**.
2. Adds the **new public key** to the `~/.ssh/authorized_keys` file.
3. Validates that the new key works.
4. Removes the **old public key**.

This ensures uninterrupted access while improving your security posture by rotating credentials safely.

---

## 🚀 Usage

```bash
ssh-update-id -i <new_private_key> -o <old_private_key> user@host [user2@host2 ...]
```

### Example:

```bash
ssh-update-id -i ~/.ssh/id_rsa_new -o ~/.ssh/id_rsa_old user@server.com
```

You can target multiple hosts in one go:

```bash
ssh-update-id -i ~/.ssh/id_rsa_new -o ~/.ssh/id_rsa_old user@host1 user@host2 user@host3
```

---

## 📋 Requirements

* Bash (strict mode compatible)
* `ssh` and `scp` installed and accessible
* Valid key files with appropriate permissions
* SSH access to the remote hosts using the **old key**

---

## 🛡️ Safe by design

* Verifies that the new and old keys are different
* Adds the new key **before** removing the old one
* Skips replacement if the new key is already installed
* Handles multiple target hosts safely
* Leaves comments in new keys intact
* ⚠️ Note: if a key appears with restrictions like `from="..."` or `command="..."`, removing the key will also remove those constraints — see next section

---

## 🧩 Use cases

* Rotating SSH keys periodically as part of your **security policy**
* Updating access after regenerating keys or certificates
* Changing personal or team access to shared servers
* Ensuring key changes are automated and **zero-downtime**

---

## ⚠️ Caveat: lines with `from=` or `command=` options

This script assumes that the public keys in `authorized_keys` are either plain or have comments only. If a key is associated with special SSH options — such as:

* `from="192.168.1.0/24"` (restrict source IPs)
* `command="/usr/local/bin/readonly-shell"` (force command on login)

— removing that key will also remove its restrictions.

If multiple entries exist for the same key (same `keytype keydata`) but with different options, **the script will delete all of them**.

👉 While this is often desirable for cleanup, it may unintentionally remove security constraints. Use with care in hardened environments.


---

## 💡 Tip

You can use this script in cron jobs, CI/CD pipelines, or during onboarding/offboarding of collaborators. It’s ideal for DevOps and sysadmin tasks.

---

## 📄 License

This project is released under [The Unlicense](https://unlicense.org/), a license that dedicates your work to the public domain.

## You are free to use, modify, and distribute it without restriction. No attribution required — though it’s appreciated!

---

## 🤝 Contributing

Pull requests and issues are welcome. Let's make SSH key rotation a painless task for everyone.




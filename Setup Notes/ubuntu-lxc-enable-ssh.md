# Enable Root Login for SSH and Access LXC Containers

This guide explains how to enable root login over SSH, which is often disabled by default for security reasons. This is particularly useful when attempting to SSH into LXC containers or remote Linux servers as the `root` user.

---

## 🔐 Problem

By default, many systems disable SSH access for the root user by setting `PermitRootLogin no` in the SSH configuration file. This can prevent direct SSH access as root.

---

## ✅ Solution: Enable `PermitRootLogin`

### Step 1: Login as Root

First, log in to your server or LXC container console as the root user. You may need to use a hypervisor console or privileged user with `sudo` access.

### Step 2: Edit SSH Configuration

Open the SSH daemon configuration file using `vi` or your preferred text editor:

```bash
nano /etc/ssh/sshd_config
```
### Step 3: Update PermitRootLogin
Find the following line:

```bash
PermitRootLogin yes
StrictModes yes
```
### Step 4: Restart SSH Service
To apply the changes, restart the SSH service:

```bash
systemctl restart sshd
```

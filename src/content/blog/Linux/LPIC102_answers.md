# LPIC-102 Answers (Linux Project)

A practical, deployment-ready markdown reference for LPIC-1 Exam 102 topics.

---

## 105. Shells, Scripting, and Data Management

### 1) What is the difference between login and non-login shells?

- **Login shell** reads `/etc/profile` and one of `~/.bash_profile`, `~/.bash_login`, or `~/.profile`.
- **Non-login interactive shell** reads `~/.bashrc`.
- Best practice: source `~/.bashrc` from `~/.bash_profile`.

### 2) How do startup files load in Bash?

```bash
# ~/.bash_profile
[ -f ~/.bashrc ] && . ~/.bashrc
```

### 3) Common shell variables and purpose

- `PATH`: executable search path
- `HOME`: user home directory
- `PS1`: primary prompt format
- `LANG` / `LC_*`: locale settings
- `HISTSIZE` / `HISTFILESIZE`: history limits

### 4) How to set and export variables?

```bash
MYVAR="hello"
export MYVAR
```

### 5) Basic shell script template

```bash
#!/usr/bin/env bash
set -euo pipefail

name="${1:-world}"
echo "Hello, $name"
```

### 6) Positional params and special params

- `$0`: script name
- `$1..$9`: arguments
- `$#`: number of args
- `$@`: all args (safe quoted as `"$@"`)
- `$?`: previous command exit code

### 7) Conditionals and loops examples

```bash
if [[ -f /etc/passwd ]]; then
  echo "exists"
fi

for u in $(cut -d: -f1 /etc/passwd); do
  echo "$u"
done

while read -r line; do
  echo "$line"
done < file.txt
```

### 8) Text processing essentials

- `grep`: pattern match
- `sed`: stream edits
- `awk`: column-based processing
- `cut`, `sort`, `uniq`, `tr`, `wc`, `paste`, `join`

Examples:

```bash
grep -R "ERROR" /var/log
sed -n '1,20p' file
awk -F: '{print $1,$3}' /etc/passwd
sort file | uniq -c | sort -nr
```

### 9) Redirection and pipes

- `>` overwrite, `>>` append
- `2>` stderr, `&>` stdout+stderr
- `|` pipe output to next command

```bash
command >out.txt 2>err.txt
command &>all.txt
cat access.log | grep 500 | wc -l
```

### 10) `find` and `xargs` usage

```bash
find /var/log -type f -name "*.log" -mtime +7
find . -type f -print0 | xargs -0 grep -n "TODO"
```

---

## 106. User Interfaces and Desktops

### 1) X11 core components

- **X server**: handles display/input
- **X client**: GUI application
- **Display manager**: login screen (gdm, lightdm, sddm)
- **Window manager/Desktop environment**: i3, GNOME, KDE

### 2) Display variables and remote X

- `DISPLAY=:0` local display
- SSH X11 forwarding:

```bash
ssh -X user@host
ssh -Y user@host   # trusted forwarding
```

### 3) Accessibility to troubleshoot GUI startup

- Check display manager status (`systemctl status gdm` etc.)
- Check logs (`journalctl -u gdm -b`)
- Validate GPU/driver issues (`dmesg`, Xorg logs)

---

## 107. Administrative Tasks

### 1) Manage users and groups

```bash
sudo useradd -m -s /bin/bash alice
sudo passwd alice
sudo usermod -aG sudo,docker alice
sudo userdel -r alice

sudo groupadd devops
sudo gpasswd -a alice devops
```

### 2) Password aging and policy

```bash
sudo chage -l alice
sudo chage -M 90 -m 7 -W 14 alice
```

### 3) `sudo` basics

- Edit safely with `visudo`
- Example rule:

```text
alice ALL=(ALL:ALL) ALL
```

### 4) Process management

```bash
ps aux | grep nginx
top
htop
pgrep sshd
kill -TERM <pid>
kill -9 <pid>
nice -n 10 long_task
renice -n -5 -p <pid>
```

### 5) Schedule jobs: `cron` and `at`

```bash
crontab -e
# m h dom mon dow command
0 2 * * * /usr/local/bin/backup.sh

at now + 30 minutes
```

### 6) Localization and time

```bash
timedatectl
timedatectl set-timezone Asia/Tokyo
locale
localectl set-locale LANG=en_US.UTF-8
```

### 7) Print systems (CUPS)

- Queue mgmt: `lpq`, `lprm`
- Print file: `lp file.txt`
- Check daemon: `systemctl status cups`

---

## 108. Essential System Services

### 1) systemd service operations

```bash
systemctl status ssh
systemctl start ssh
systemctl enable ssh
systemctl restart ssh
journalctl -u ssh -b
```

### 2) Boot targets and rescue mode

```bash
systemctl get-default
systemctl set-default multi-user.target
systemctl isolate rescue.target
```

### 3) Logging

- Traditional: `/var/log/*`
- systemd journal:

```bash
journalctl -xe
journalctl --since "today"
journalctl -u nginx --since "1 hour ago"
```

### 4) Mail Transfer Agent basics

- Common MTAs: Postfix, Exim
- Queue and status checks depend on MTA (`postqueue -p`, etc.)

### 5) Time sync

```bash
timedatectl status
systemctl status systemd-timesyncd
```

(Or Chrony: `chronyc sources -v`)

---

## 109. Networking Fundamentals

### 1) Interface/IP inspection

```bash
ip a
ip r
ss -tulpen
```

### 2) Configure temporary IP

```bash
sudo ip addr add 192.168.1.50/24 dev eth0
sudo ip route add default via 192.168.1.1
```

### 3) DNS resolution checks

```bash
cat /etc/resolv.conf
getent hosts example.com
dig example.com +short
host example.com
```

### 4) Network troubleshooting flow

1. `ip a` (interface up?)
2. `ip r` (route exists?)
3. `ping gateway`
4. `ping 8.8.8.8`
5. `ping example.com` (DNS)
6. `traceroute example.com`
7. `ss -tulpen` (ports/services)

### 5) Common client tools

- `ssh`, `scp`, `sftp`
- `curl`, `wget`
- `nc`/`ncat` for quick socket tests

---

## 110. Security

### 1) File permissions and ownership

```bash
chmod 640 file
chmod u+x script.sh
chown alice:devops file
```

### 2) Special permission bits

- **SUID** (`4`): run as file owner
- **SGID** (`2`): run as group / directory group inheritance
- **Sticky** (`1`): only owner/root can delete in dir (e.g. `/tmp`)

```bash
chmod 4755 /path/bin
chmod 2775 /shared/dir
chmod 1777 /tmp-like-dir
```

### 3) Default permissions with umask

```bash
umask
umask 027
```

### 4) Basic host hardening checklist

- Disable direct root SSH login (`PermitRootLogin no`)
- Enforce key auth, disable password auth where possible
- Keep packages updated
- Enable firewall (`ufw`/`nftables`/`firewalld`)
- Remove unused services
- Audit logs regularly

### 5) OpenSSH client/server essentials

- Server config: `/etc/ssh/sshd_config`
- Restart service after changes:

```bash
sudo sshd -t && sudo systemctl restart ssh
```

### 6) GPG basics

```bash
gpg --full-generate-key
gpg --list-keys
gpg -e -r "Alice" secret.txt
gpg -d secret.txt.gpg
```

---

## High-Yield Command Cheat Sheet

```bash
# users/groups
useradd usermod userdel groupadd passwd chage id

# files/text
find grep sed awk cut sort uniq xargs tar gzip bzip2 xz

# processes/services
ps top kill pkill pgrep nice renice systemctl journalctl

# networking
ip ss ping traceroute dig host curl wget ssh scp

# security
chmod chown chgrp umask sudo visudo ssh-keygen gpg
```

---

## Exam Strategy (LPIC-102)

1. Practice command syntax from memory.
2. Focus on **real admin workflows** (not just definitions).
3. Memorize paths and config files (`/etc/passwd`, `/etc/shadow`, `/etc/ssh/sshd_config`, etc.).
4. Get comfortable with shell pipelines and text filtering.
5. In scenario questions: troubleshoot bottom-up (local → network → service).

---

## Optional: Add This to Your Site Navigation

If your site generator supports front matter, prepend this block:

```yaml
---
title: LPIC-102 Answers
description: Practical LPIC-1 102 reference for Linux admin tasks.
---
```

Done: this file is ready to publish as `LPIC102_answers.md`.

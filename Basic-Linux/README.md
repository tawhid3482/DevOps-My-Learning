# 🐧 Linux Mastery Roadmap (DevOps & Interview Ready)

> **লক্ষ্য:** Linux এর মৌলিক ধারণা থেকে DevOps engineer-দের daily-use ও interview-ready topics — সব এক জায়গায়।  
> ভাষা: বাংলা + English (interview lines)

---

## 📑 Table of Contents

| # | Topic |
|---|-------|
| 1 | [Linux কী & DevOps-এ কেন গুরুত্বপূর্ণ](#-1-linux-কী--devops-এ-কেন-গুরুত্বপূর্ণ) |
| 2 | [Linux File System Structure](#-2-linux-file-system-structure-খুব-গুরুত্বপূর্ণ) |
| 3 | [Navigation & File Operations](#-3-navigation--file-operations) |
| 4 | [File Permissions (Interview Hot)](#-4-file-permissions-interview-hot) |
| 5 | [Text Processing & Search](#-5-text-processing--search) |
| 6 | [Process Management](#-6-process-management) |
| 7 | [System Monitoring (CPU, RAM, Disk)](#-7-system-monitoring-cpu-ram-disk) |
| 8 | [Networking Commands](#-8-networking-commands) |
| 9 | [Package Management](#-9-package-management) |
| 10 | [systemd & Service Management](#-10-systemd--service-management) |
| 11 | [Logs & Troubleshooting](#-11-logs--troubleshooting) |
| 12 | [SSH & Remote Access](#-12-ssh--remote-access) |
| 13 | [Users, Groups & sudo](#-13-users-groups--sudo) |
| 14 | [Cron Jobs & Automation](#-14-cron-jobs--automation) |
| 15 | [Environment Variables & Shell](#-15-environment-variables--shell) |
| 16 | [Pipes, Redirects & Exit Codes](#-16-pipes-redirects--exit-codes) |
| 17 | [Compression & Transfer](#-17-compression--transfer) |
| 18 | [Firewall Basics](#-18-firewall-basics) |
| 19 | [DevOps Troubleshooting Scenarios](#-19-devops-troubleshooting-scenarios-interview-favorite) |
| 20 | [Most Important Commands](#-20-most-important-commands-full-explanation-in-bangla) |
| 21 | [Quick Cheat Sheet](#-21-quick-cheat-sheet) |

---

## 🧠 1. Linux কী & DevOps-এ কেন গুরুত্বপূর্ণ

### ❓ Linux কী?

**Linux** হলো একটি open-source **Unix-like operating system kernel**। DevOps world-এ servers, containers, cloud (AWS, GCP, Azure), CI/CD pipelines — সবখানেই Linux dominate করে।

| ক্ষেত্র | Linux ব্যবহার |
|--------|---------------|
| Cloud servers | EC2, GCE, Azure VM — সব Linux-based |
| Containers | Docker, Kubernetes — Linux kernel features |
| CI/CD | Jenkins, GitHub Actions runners — Linux |
| Infrastructure | Terraform, Ansible — Linux servers manage |

### 🔥 Linux vs Windows (Server context)

| Feature | Linux | Windows Server |
|---------|-------|----------------|
| Cost | Free / Open source | License required |
| CLI | Powerful (default) | PowerShell |
| DevOps adoption | Industry standard | Specific use cases |
| Scripting | Bash, Python | PowerShell |
| Containers | Native support | Limited |

> **📌 Interview line:**  
> *"Most production servers and cloud infrastructure run on Linux because of stability, security, flexibility, and strong CLI tooling for automation."*

---

## 📂 2. Linux File System Structure (খুব গুরুত্বপূর্ণ)

Linux এ সব কিছু **file** হিসেবে treat হয় — even devices ও processes।

### 🗂️ Important Directories

| Path | উদ্দেশ্য | DevOps relevance |
|------|---------|------------------|
| `/` | Root — সব directory এর শুরু | System base |
| `/home` | User home directories | App configs, user data |
| `/etc` | Configuration files | nginx.conf, sshd_config |
| `/var` | Variable data (logs, cache) | `/var/log`, `/var/www` |
| `/var/log` | System & app logs | **Troubleshooting hub** |
| `/tmp` | Temporary files | Cleared on reboot |
| `/usr` | User programs & binaries | Installed software |
| `/bin`, `/sbin` | Essential system binaries | `ls`, `cp`, `systemctl` |
| `/opt` | Optional/third-party software | Custom apps |
| `/proc` | Virtual filesystem — process info | `cat /proc/cpuinfo` |
| `/dev` | Device files | Disks, terminals |

> **📌 Interview line:**  
> *"`/etc` for configuration, `/var/log` for logs, `/home` for user data, and `/proc` for runtime process information."*

### 🔗 Hard Link vs Soft Link (Symbolic Link)

| Type | Command | Behavior |
|------|---------|----------|
| **Hard link** | `ln file hardlink` | Same inode, original delete হলেও data থাকে |
| **Soft link** | `ln -s file symlink` | Shortcut — original delete হলে broken link |

```bash
ln file.txt hardlink.txt       # hard link
ln -s /path/to/file symlink    # soft/symbolic link
ls -l                          # link দেখতে
```

---

## 📁 3. Navigation & File Operations

### 🧭 Navigation

```bash
pwd                 # Print Working Directory — বর্তমান location
ls                  # list files
ls -l               # detailed (permissions, size, date)
ls -la              # hidden files সহ ( .git, .env )
ls -lh              # human-readable size (KB, MB)

cd folder_name      # folder এ যাও
cd ..               # এক level up
cd ~                # home directory
cd /                # root directory
cd -                # আগের directory তে ফিরে যাও
```

### 📄 File & Directory Create/Read/Delete

```bash
# Create
mkdir project
mkdir -p app/src/components    # nested folders একসাথে
touch file.txt                 # empty file
touch a.txt b.txt c.txt        # multiple files

# Read
cat file.txt                   # পুরো file
less file.txt                  # paginated (বড় file)
head -n 20 file.txt            # প্রথম 20 lines
tail -n 50 file.log            # শেষ 50 lines
tail -f /var/log/syslog        # real-time log (DevOps favorite)
nl file.txt                    # line numbers সহ

# Copy / Move / Delete
cp file.txt backup.txt
cp -r folder1 folder2          # recursive folder copy
mv old.txt new.txt               # rename
mv file.txt /home/ubuntu/        # move
rm file.txt
rm -r folder                     # folder delete
rm -rf folder                    # force delete ⚠️ সতর্ক!
```

### ✏️ Text Editors

```bash
nano file.txt       # beginner friendly — Ctrl+O save, Ctrl+X exit
vim file.txt        # advanced — :wq save & quit, :q! quit without save
```

> **📌 Interview tip:** Production server এ `vim`/`nano` দিয়ে config edit করা common — practice করো।

---

## 🔐 4. File Permissions (Interview Hot)

### 🧩 Permission Structure

```bash
ls -l
# -rwxr-xr-x  1 ubuntu ubuntu  4096 Jan 10  app.sh
#  │││││││││
#  │└┴┴┴┴┴┴┴── permissions (owner/group/others)
#  └────────── file type (- = file, d = directory)
```

| Position | Meaning | Values |
|----------|---------|--------|
| 1st char | Type | `-` file, `d` directory, `l` link |
| Owner (u) | File owner | `r` read, `w` write, `x` execute |
| Group (g) | Group members | same |
| Others (o) | Everyone else | same |

### 🔢 Numeric (Octal) Permissions

| Number | Permission |
|--------|------------|
| 4 | read (r) |
| 2 | write (w) |
| 1 | execute (x) |

```bash
chmod 755 script.sh     # rwxr-xr-x — owner full, others read+execute
chmod 644 file.txt      # rw-r--r-- — owner read+write, others read only
chmod +x script.sh      # executable করো
chmod -R 755 folder/    # recursive

chown ubuntu file.txt           # owner change
chown ubuntu:devops file.txt    # owner + group
chown -R ubuntu:ubuntu folder/  # recursive
```

### Common Permission Sets (DevOps)

| Permission | Meaning | Use case |
|------------|---------|----------|
| `755` | rwxr-xr-x | Scripts, executables |
| `644` | rw-r--r-- | Config files, static content |
| `600` | rw------- | Private keys, secrets |
| `777` | rwxrwxrwx | ⚠️ Avoid in production |

> **📌 Interview line:**  
> *"755 for executables, 644 for config files, and 600 for sensitive files like SSH private keys."*

---

## 🔍 5. Text Processing & Search

### grep — Pattern Search

```bash
grep "error" app.log              # search text
grep -i "error" app.log           # case insensitive
grep -r "TODO" ./src              # recursive search
grep -n "error" app.log           # line numbers সহ
grep -v "debug" app.log           # exclude lines
grep -c "ERROR" app.log           # count matches

# DevOps classic combo
tail -f app.log | grep ERROR
journalctl -u nginx -f | grep "502"
```

### find — File Search

```bash
find . -name "*.log"                    # by name
find /var/log -name "*.log" -mtime -7   # modified last 7 days
find . -type f -size +100M              # files > 100MB
find . -name "*.tmp" -delete            # find & delete
find /home -user ubuntu                 # by owner
```

### sed & awk (Basics)

```bash
# sed — stream editor
sed 's/old/new/g' file.txt              # replace all
sed -i 's/old/new/g' file.txt           # in-place replace
sed -n '10,20p' file.txt                # lines 10-20 print

# awk — column processing
awk '{print $1}' file.txt               # first column
ps aux | awk '{print $2, $11}'          # PID + command
df -h | awk 'NR>1 {print $5, $6}'       # disk usage % + mount
```

### wc, sort, uniq

```bash
wc -l file.txt                # line count
sort file.txt                 # sort lines
sort -u file.txt              # unique sorted
uniq -c file.txt              # duplicate count (sorted input needed)
```

---

## ⚙️ 6. Process Management

### Process দেখা

```bash
ps                            # current terminal processes
ps aux                        # all processes (detailed)
ps aux | grep nginx           # specific process
pgrep nginx                   # PID by name
top                           # live process monitor
htop                          # better UI (install: apt install htop)
```

### Process Kill & Signals

```bash
kill PID                      # graceful stop (SIGTERM = 15)
kill -9 PID                   # force kill (SIGKILL = 9)
kill -HUP PID                 # reload config (SIGKILL = 1)
killall nginx                 # by process name
pkill -f "python app.py"      # by pattern

# Background / Foreground
command &                     # background run
jobs                          # background jobs list
fg %1                         # foreground এ আনা
nohup command &               # terminal close হলেও চলবে
```

| Signal | Number | Meaning |
|--------|--------|---------|
| SIGHUP | 1 | Hangup — reload |
| SIGTERM | 15 | Graceful termination |
| SIGKILL | 9 | Force kill (cannot be caught) |

> **📌 Interview line:**  
> *"SIGTERM allows graceful shutdown; SIGKILL forcefully terminates immediately. Always try SIGTERM first."*

### Process Priority

```bash
nice -n 10 command            # lower priority start
renice -n 5 -p PID            # running process priority change
```

---

## 📊 7. System Monitoring (CPU, RAM, Disk)

### Memory

```bash
free -h                       # RAM & swap usage
# Output: total, used, free, available, swap

cat /proc/meminfo             # detailed memory info
```

### Disk

```bash
df -h                         # filesystem disk usage
df -h /                       # root partition
du -sh folder/                # folder size
du -sh * | sort -hr           # largest items in current dir
lsblk                         # block devices (disks)
fdisk -l                      # partition info (needs sudo)
```

### CPU & Load

```bash
uptime                        # load average (1, 5, 15 min)
cat /proc/cpuinfo             # CPU info
nproc                         # CPU core count
lscpu                         # CPU summary
vmstat 1 5                    # virtual memory stats (1 sec interval, 5 times)
iostat -x 1                   # disk I/O stats (sysstat package)
```

### Load Average বোঝা

```
load average: 1.20, 0.80, 0.50
```

| Load vs CPU cores | Meaning |
|-------------------|---------|
| Load ≈ cores | System busy but OK |
| Load > cores | Processes waiting — bottleneck |
| Load >> cores | Overloaded — investigate |

> **📌 Interview line:**  
> *"Load average shows runnable processes. Compare it with CPU core count — if load exceeds cores, the system is overloaded."*

---

## 🌐 8. Networking Commands

```bash
ip a                          # IP addresses (modern)
ip addr show
hostname -I                   # quick IP check
ifconfig                      # legacy (may need net-tools)

ping google.com               # connectivity test
ping -c 4 google.com          # 4 packets only

# Port & connection check
ss -tulpn                     # listening ports (modern)
netstat -tulpn                # legacy equivalent
lsof -i :80                   # what's using port 80
lsof -i :443

# DNS
nslookup google.com
dig google.com
host google.com

# Route
traceroute google.com
tracepath google.com

# Download
curl -I https://google.com    # headers only
curl -O https://example.com/file.zip
wget https://example.com/file.zip
wget -c URL                   # resume download
```

### curl vs wget

| Tool | Best for |
|------|----------|
| **curl** | API testing, headers, HTTP methods |
| **wget** | File download, recursive mirror |

```bash
# DevOps API testing
curl -X GET https://api.example.com/health
curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' URL
```

---

## 📦 9. Package Management

### Ubuntu/Debian (apt)

```bash
sudo apt update               # package list update
sudo apt upgrade              # installed packages upgrade
sudo apt install nginx        # install
sudo apt remove nginx         # remove
sudo apt purge nginx          # remove + config files
sudo apt autoremove           # unused dependencies clean
apt search nginx              # search package
apt show nginx                # package info
dpkg -l | grep nginx          # installed packages list
```

### RHEL/CentOS/Amazon Linux (yum/dnf)

```bash
sudo yum update
sudo yum install nginx
sudo yum remove nginx
sudo dnf install nginx        # newer RHEL/Fedora
rpm -qa | grep nginx          # installed RPM packages
```

> **📌 Interview line:**  
> *"apt for Debian/Ubuntu, yum/dnf for RHEL/CentOS/Amazon Linux — always run update before install in automation scripts."*

---

## 🔧 10. systemd & Service Management

**systemd** = modern Linux service manager (init system replacement)

```bash
sudo systemctl status nginx       # service status
sudo systemctl start nginx        # start
sudo systemctl stop nginx         # stop
sudo systemctl restart nginx      # restart
sudo systemctl reload nginx       # reload config (no downtime)
sudo systemctl enable nginx       # boot এ auto-start
sudo systemctl disable nginx      # auto-start বন্ধ
sudo systemctl is-active nginx    # running কিনা check
sudo systemctl list-units --type=service   # all services

# Failed services
sudo systemctl --failed
```

### Service Unit File Location

```
/etc/systemd/system/        # custom/admin units
/lib/systemd/system/        # package-installed units
```

```bash
sudo systemctl daemon-reload      # unit file change পর reload
sudo journalctl -u nginx -f       # service logs live
```

> **📌 Interview line:**  
> *"systemctl manages services; enable for boot startup, start/stop/restart for runtime control, and journalctl for logs."*

---

## 📋 11. Logs & Troubleshooting

### Log Locations

| Log | Path | Content |
|-----|------|---------|
| System log | `/var/log/syslog` | General system events |
| Auth log | `/var/log/auth.log` | Login, sudo attempts |
| Nginx | `/var/log/nginx/access.log` | HTTP requests |
| Nginx error | `/var/log/nginx/error.log` | Nginx errors |
| Kernel | `/var/log/kern.log` | Kernel messages |

### journalctl (systemd logs)

```bash
journalctl                        # all logs
journalctl -u nginx               # specific service
journalctl -u nginx -f            # follow (live)
journalctl -u nginx --since "1 hour ago"
journalctl -u nginx --since today
journalctl -p err                 # error level only
journalctl -b                     # current boot logs
journalctl -b -1                  # previous boot
dmesg                             # kernel ring buffer
dmesg | tail -20
```

### Troubleshooting Flow

```
1. Symptom identify → service down? slow? error?
2. systemctl status <service>
3. journalctl -u <service> -n 50
4. tail -f /var/log/...
5. Check resources: free -h, df -h, top
6. Check network: ss -tulpn, curl health endpoint
7. Fix → restart service → verify
```

---

## 🔑 12. SSH & Remote Access

```bash
# Connect
ssh user@ip-address
ssh -p 2222 user@ip-address     # custom port
ssh -i mykey.pem ubuntu@54.12.34.56

# Key generate
ssh-keygen -t ed25519 -C "your@email.com"
ssh-keygen -t rsa -b 4096

# Copy public key to server
ssh-copy-id user@server

# Config file (~/.ssh/config)
Host myserver
    HostName 54.12.34.56
    User ubuntu
    IdentityFile ~/.mykey.pem
    Port 22

# Then simply:
ssh myserver
```

### SSH Key Permissions (Important!)

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa          # private key
chmod 644 ~/.ssh/id_rsa.pub      # public key
chmod 600 ~/.ssh/authorized_keys
```

### SCP — File Transfer

```bash
scp file.txt user@server:/path/
scp -r folder/ user@server:/path/
scp user@server:/remote/file.txt ./local/
```

> **📌 Interview line:**  
> *"SSH keys are preferred over passwords. Private key must be 600 permissions, and authorized_keys on server for access."*

---

## 👥 13. Users, Groups & sudo

```bash
whoami                          # current user
id                              # user ID, groups
w                               # logged in users
last                            # login history

# User management (root/sudo)
sudo useradd -m -s /bin/bash newuser
sudo passwd newuser
sudo usermod -aG sudo newuser   # add to sudo group
sudo userdel -r username        # delete user + home

# Groups
groups                          # my groups
sudo groupadd devops
sudo usermod -aG devops username

# sudo
sudo command                    # run as root
sudo -i                         # root shell
sudo -u otheruser command       # as specific user
visudo                          # edit sudoers safely
```

### /etc/passwd & /etc/shadow

| File | Contains |
|------|----------|
| `/etc/passwd` | User accounts (readable) |
| `/etc/shadow` | Encrypted passwords (root only) |
| `/etc/group` | Group definitions |

---

## ⏰ 14. Cron Jobs & Automation

**Cron** = scheduled task runner

```bash
crontab -e                      # edit my cron jobs
crontab -l                      # list my cron jobs
crontab -r                      # remove all (careful!)

# System-wide
sudo nano /etc/crontab
ls /etc/cron.d/
ls /etc/cron.daily/
```

### Cron Syntax

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7, Sun=0)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

| Example | Meaning |
|---------|---------|
| `0 2 * * *` | Every day at 2:00 AM |
| `*/5 * * * *` | Every 5 minutes |
| `0 0 * * 0` | Every Sunday midnight |
| `0 9-17 * * 1-5` | Weekdays 9 AM–5 PM hourly |

```bash
# Cron logs
grep CRON /var/log/syslog
journalctl -u cron
```

---

## 🌍 15. Environment Variables & Shell

```bash
env                             # all environment variables
echo $PATH                      # specific variable
echo $HOME
echo $USER
echo $SHELL

export PORT=5000                # set for current session
export APP_ENV=production

# Permanent (add to ~/.bashrc or ~/.profile)
echo 'export PORT=5000' >> ~/.bashrc
source ~/.bashrc                # reload

# PATH add
export PATH=$PATH:/opt/myapp/bin
```

### Important Variables (DevOps)

| Variable | Purpose |
|----------|---------|
| `$PATH` | Command search paths |
| `$HOME` | User home directory |
| `$USER` | Current username |
| `$PWD` | Current directory |
| `$?` | Last command exit code |

---

## 🔀 16. Pipes, Redirects & Exit Codes

### Redirects

```bash
command > file.txt              # stdout to file (overwrite)
command >> file.txt             # stdout append
command 2> error.log            # stderr to file
command &> all.log              # stdout + stderr
command > out.log 2>&1          # both to same file
command < input.txt             # read from file
```

### Pipes

```bash
command1 | command2             # stdout → stdin
ps aux | grep nginx
cat file.log | wc -l
curl -s URL | jq '.status'
```

### Exit Codes

```bash
echo $?                         # last command exit code
# 0 = success
# non-zero = error

# Script example
command
if [ $? -eq 0 ]; then
    echo "Success"
else
    echo "Failed"
fi
```

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 2 | Misuse of command |
| 126 | Command not executable |
| 127 | Command not found |
| 130 | Terminated by Ctrl+C |

> **📌 Interview line:**  
> *"Exit code 0 means success; non-zero indicates failure. In CI/CD scripts we check `$?` or use `set -e` to fail on errors."*

### Useful Script Header

```bash
#!/bin/bash
set -e          # exit on any error
set -u          # error on undefined variable
set -o pipefail # pipe failure detect
```

---

## 📦 17. Compression & Transfer

```bash
# tar (most common in DevOps)
tar -cvf archive.tar folder/          # create
tar -czvf archive.tar.gz folder/        # create + gzip compress
tar -xzvf archive.tar.gz                # extract gzip
tar -xvf archive.tar                    # extract

# zip
zip -r backup.zip project/
unzip backup.zip

# gzip
gzip file.txt                           # compress → file.txt.gz
gunzip file.txt.gz                      # decompress
```

| Extension | Command |
|-----------|---------|
| `.tar` | `tar -cvf` / `tar -xvf` |
| `.tar.gz` / `.tgz` | `tar -czvf` / `tar -xzvf` |
| `.zip` | `zip -r` / `unzip` |
| `.gz` | `gzip` / `gunzip` |

---

## 🛡️ 18. Firewall Basics

### UFW (Ubuntu)

```bash
sudo ufw status
sudo ufw enable
sudo ufw allow 22                   # SSH
sudo ufw allow 80                   # HTTP
sudo ufw allow 443                  # HTTPS
sudo ufw allow from 10.0.0.0/8      # specific network
sudo ufw deny 3306                  # block MySQL external
sudo ufw delete allow 80
```

### firewalld (RHEL/CentOS)

```bash
sudo firewall-cmd --list-all
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

> **📌 Interview line:**  
> *"UFW on Ubuntu, firewalld on RHEL. Always allow SSH (port 22) before enabling firewall to avoid lockout."*

---

## 🚨 19. DevOps Troubleshooting Scenarios (Interview Favorite)

### Scenario 1: Server slow / high load

```bash
uptime                    # load average check
top / htop                # CPU/RAM hog process
free -h                   # memory
df -h                     # disk full?
iostat -x 1               # disk I/O bottleneck
ps aux --sort=-%mem | head   # top memory processes
ps aux --sort=-%cpu | head   # top CPU processes
```

### Scenario 2: Disk full

```bash
df -h                     # which partition full
du -sh /* 2>/dev/null | sort -hr | head   # largest dirs
du -sh /var/log/* | sort -hr              # log size
journalctl --disk-usage                   # journal size
sudo journalctl --vacuum-size=500M        # clean journal
find /var/log -name "*.gz" -delete        # old compressed logs
```

### Scenario 3: Service won't start

```bash
sudo systemctl status nginx
sudo journalctl -u nginx -n 50 --no-pager
sudo nginx -t                           # config syntax test
ss -tulpn | grep :80                    # port already in use?
cat /etc/nginx/nginx.conf
```

### Scenario 4: Port already in use

```bash
ss -tulpn | grep :8080
lsof -i :8080
kill $(lsof -t -i:8080)                 # kill process on port
```

### Scenario 5: Permission denied

```bash
ls -la file
id
groups
sudo chown $USER:$USER file
chmod 644 file
```

### Scenario 6: Cannot connect to server

```bash
ping server-ip
telnet server-ip 22           # or nc -zv server-ip 22
ssh -v user@server            # verbose SSH debug
traceroute server-ip
sudo ufw status
```

---

## 🚀 20. Most Important Commands (Full Explanation in Bangla)

---

### 1. `pwd` — Print Working Directory

```bash
pwd
# Output: /home/ubuntu/project
```

বর্তমানে কোন folder-এ আছো সেটা দেখায়।

---

### 2. `ls` — List Files

```bash
ls -la    # DevOps daily driver — hidden + details
```

---

### 3. `cd` — Change Directory

```bash
cd project && pwd
```

---

### 4. `mkdir` / `touch`

```bash
mkdir -p app/logs
touch deploy.sh
```

---

### 5. `cat` / `tail -f`

```bash
cat /etc/os-release
tail -f /var/log/nginx/access.log
```

---

### 6. `grep`

```bash
grep -r "error" /var/log/
tail -f app.log | grep -i "exception"
```

---

### 7. `find`

```bash
find /var/log -name "*.log" -mtime +30
```

---

### 8. `chmod` / `chown`

```bash
chmod 600 ~/.ssh/id_rsa
chown www-data:www-data /var/www/html
```

---

### 9. `ps` / `kill`

```bash
ps aux | grep java
kill -15 PID    # graceful first
kill -9 PID     # force if needed
```

---

### 10. `top` / `htop`

Live system monitor — CPU, memory, processes।

---

### 11. `free -h` / `df -h`

```bash
free -h     # RAM
df -h       # Disk
du -sh *    # folder sizes
```

---

### 12. `systemctl`

```bash
sudo systemctl restart nginx && sudo systemctl status nginx
```

---

### 13. `journalctl`

```bash
journalctl -u docker -f --since "30 min ago"
```

---

### 14. `curl` / `wget`

```bash
curl -sf http://localhost/health || echo "Service down"
wget -q URL -O file.tar.gz
```

---

### 15. `ssh` / `scp`

```bash
ssh -i key.pem ubuntu@server
scp -r ./app ubuntu@server:/opt/
```

---

### 16. `tar`

```bash
tar -czvf backup-$(date +%F).tar.gz /var/www
tar -xzvf backup.tar.gz
```

---

### 17. `crontab`

```bash
crontab -l
# 0 3 * * * /opt/scripts/backup.sh
```

---

### 18. `history` & Shortcuts

```bash
history | grep nginx
!!              # repeat last command
!25             # run command #25 from history
```

| Shortcut | Action |
|----------|--------|
| `Tab` | Auto-complete |
| `↑` / `↓` | Previous/next command |
| `Ctrl + C` | Stop running command |
| `Ctrl + Z` | Suspend process |
| `Ctrl + L` | Clear screen |
| `Ctrl + R` | Reverse search history |

---

## 📋 21. Quick Cheat Sheet

### Daily DevOps Workflow

```bash
ssh user@server
cd /opt/app
git pull
sudo systemctl restart app
journalctl -u app -f
tail -f /var/log/app/error.log
```

### File Permission Quick Reference

```
r=4  w=2  x=1
755 = rwxr-xr-x  (scripts)
644 = rw-r--r--  (configs)
600 = rw-------  (secrets)
```

### Top 20 DevOps Commands

```bash
ls -la          cd              pwd
mkdir -p        rm -rf          cp -r
mv              cat             nano/vim
grep            find            tail -f
ps aux          top/htop        free -h
df -h           ip a / ss       curl/wget
systemctl       journalctl      ssh/scp
chmod/chown     tar             crontab
```

### Golden Rules

| Rule | কারণ |
|------|-------|
| Production এ `rm -rf` সতর্কতায় | Data loss irreversible |
| SSH key permission `600` রাখো | Security requirement |
| Firewall enable করার আগে SSH allow | Lockout prevention |
| `kill -9` শেষ option | Graceful shutdown first |
| Log rotate/monitor করো | Disk full prevention |
| Script এ `set -e` ব্যবহার করো | Silent failure avoid |
| Config change এর backup নাও | Rollback possible |

### Common Interview Q&A

| Question | Short Answer |
|----------|--------------|
| PID 1 কী? | systemd (modern Linux) — parent of all processes |
| `soft link` vs `hard link`? | Soft = shortcut; Hard = same inode |
| `SIGTERM` vs `SIGKILL`? | SIGTERM graceful; SIGKILL force |
| `/etc`, `/var`, `/home`? | Config, variable data/logs, user home |
| Exit code 0? | Command success |
| Load average? | Runnable processes — compare with CPU cores |
| `curl` vs `wget`? | curl for APIs; wget for downloads |

---

<p align="center">
  <strong>Happy Learning! 🎯</strong><br>
  <em>Linux practice করো → DevOps interview crack করো</em>
</p>

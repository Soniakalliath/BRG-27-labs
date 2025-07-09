# 🐧 Linux Server Management Scripts

This document provides a collection of **Bash scripts** for managing a Linux server, including user management, system monitoring, backups, and scheduled tasks.

## 📁 Contents
1. [User & Group Management](#user--group-management)
2. [Storage & Quota](#storage--quota)
3. [Memory, Process, Network Monitoring](#memory-process-network-monitoring)
4. [Notifications & Maintenance](#notifications--maintenance)
5. [Daily Scripts](#daily-scripts)
6. [Scheduling (cron)](#scheduling-cron)

---

## 🧑‍💼 User & Group Management

### Create User & Set Password
```bash
read -p "Enter username: " username
useradd -m "$username"
passwd "$username"
```

### Create Group & Add User
```bash
read -p "Group name: " group
read -p "User to add: " user
groupadd "$group"
usermod -aG "$group" "$user"
```

### Bulk Create Users from CSV
```bash
while IFS=',' read -r username password; do
    useradd -m "$username"
    echo "$username:$password" | chpasswd
done < users.csv
```

### Set Home Directory Quota
```bash
setquota -u john 1048576 1048576 0 0 /home
```

---

## 💽 Storage & Quota

### Alert if Disk Usage >90%
```bash
df -h | grep '^/dev/' | awk '{print $5, $6}' | while read use mount; do
    if [ "${use%%%}" -gt 90 ]; then
        echo "Disk usage alert: $mount at $use"
    fi
done
```

### Alert if User Folder >90%
```bash
for dir in /home/*; do
    [ -d "$dir" ] || continue
    size=$(du -s "$dir" | awk '{print $1}')
    # logic to compute percentage here...
done
```

---

## 📉 Memory, Process, Network Monitoring

### Top 10 Memory Users
```bash
ps aux --sort=-%mem | head -n 11
```

### High CPU Processes
```bash
ps -eo pid,ppid,cmd,%cpu --sort=-%cpu | awk '$4>80'
```

### Open Ports
```bash
ss -tuln
```

### Bandwidth Snapshot
```bash
# Example: measure RX/TX per second
```

---

## 🛠 Notifications & Maintenance

### Restart Service If Down
```bash
if ! systemctl is-active --quiet nginx; then systemctl restart nginx; fi
```

### Log Backup
```bash
cp /var/log/*.log /backup/logs/
```

### DB Backup
```bash
mysqldump -u root -p mydb > /backup/mydb.sql
```

---

## 🕒 Daily Scripts

### Disk Monitoring
```bash
# See above
```

### Directory Backup
```bash
tar -czf /backup/etc_$(date +%F).tar.gz /etc
```

### Failed SSH Attempts
```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
```

### Ping Critical Servers
```bash
for s in 8.8.8.8 example.com; do ping -c 1 $s && echo "$s OK" || echo "$s FAIL"; done
```

### Clean Logs >14 Days Old
```bash
find /var/log -name "*.log" -mtime +14 -delete
```

---

## ⏰ Scheduling (cron)

### Daily at 1AM
```bash
(crontab -l ; echo "0 1 * * * /usr/local/bin/daily.sh") | crontab -
```

### One-Time with `at`
```bash
echo "/usr/local/bin/reboot.sh" | at now + 10 minutes
```
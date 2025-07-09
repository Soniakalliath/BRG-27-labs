# 🪟 Windows Server Management Scripts

This document contains **PowerShell scripts** for managing a Windows Server, covering user/group operations, backups, monitoring, and task scheduling.

## 📁 Contents
1. [User & Group Management](#user--group-management)
2. [Storage & Disk Monitoring](#storage--disk-monitoring)
3. [Memory, CPU, Network](#memory-cpu-network)
4. [Backups & Maintenance](#backups--maintenance)
5. [Daily Scripts](#daily-scripts)
6. [Scheduling (Task Scheduler)](#scheduling-task-scheduler)

---

## 🧑‍💼 User & Group Management

### Create Local User
```powershell
$Username = "jdoe"
$Password = Read-Host -AsSecureString
New-LocalUser -Name $Username -Password $Password
```

### Add to Group
```powershell
Add-LocalGroupMember -Group "Users" -Member "jdoe"
```

### Bulk Create from CSV
```powershell
Import-Csv users.csv | ForEach-Object {
    $p = ConvertTo-SecureString $_.Password -AsPlainText -Force
    New-LocalUser -Name $_.Username -Password $p
}
```

---

## 💽 Storage & Disk Monitoring

### Disk Usage >90%
```powershell
Get-PSDrive -PSProvider FileSystem | Where-Object { ($_.Used / $_.Maximum) * 100 -gt 90 }
```

### Home Folder Alerts
```powershell
# Loop through C:\Users\* and compute size, compare to drive total
```

---

## 📉 Memory, CPU, Network

### Top Memory Processes
```powershell
Get-Process | Sort-Object WorkingSet -Descending | Select -First 10
```

### High CPU Use
```powershell
Get-Process | Sort-Object CPU -Descending | Select -First 10
```

### Open Ports
```powershell
Get-NetTCPConnection | Where-Object State -eq "Listen"
```

### Network Usage Snapshot
```powershell
Get-NetAdapterStatistics | Select Name, ReceivedBytes, SentBytes
```

---

## 📂 Backups & Maintenance

### Event Log Backup
```powershell
wevtutil epl System "C:\Backups\System.evtx"
```

### SQL DB Backup (with SQL Server Module)
```powershell
Invoke-Sqlcmd -Query "BACKUP DATABASE [MyDB] TO DISK='C:\Backup\MyDB.bak'"
```

### Weekly Maintenance
```powershell
Restart-Service W3SVC
& "C:\Scripts\BackupLogs.ps1"
& "C:\Scripts\BackupDB.ps1"
```

---

## 🕒 Daily Scripts

### Directory Backup
```powershell
Compress-Archive -Path "C:\Config\*" -DestinationPath "D:\Backups\Config.zip"
```

### SSH Login Failures
```powershell
Get-EventLog -LogName Security -Newest 500 | Where-Object Message -like "*Failure*"
```

### Ping Test
```powershell
foreach ($s in "8.8.8.8","example.com") {
  if (Test-Connection $s -Count 1 -Quiet) { "$s OK" } else { "$s FAIL" }
}
```

### Clean Logs >30 Days
```powershell
Get-ChildItem "C:\Logs" -Recurse -File | Where-Object LastWriteTime -lt (Get-Date).AddDays(-30) | Remove-Item
```

---

## ⏰ Scheduling (Task Scheduler)

### Create Daily Task at 1AM
```powershell
$Action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File 'C:\Scripts\daily.ps1'"
$Trigger = New-ScheduledTaskTrigger -Daily -At 1am
Register-ScheduledTask -TaskName "DailyScript" -Action $Action -Trigger $Trigger -User "SYSTEM" -RunLevel Highest
```
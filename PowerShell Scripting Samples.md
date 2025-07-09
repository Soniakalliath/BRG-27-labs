# 3b-1 Lab: PowerShell Backup Script, Task Scheduler & Cloud Export

## Objective

Learn how to automate system backups using PowerShell scripting and Windows Task Scheduler, and export backups securely to a remote cloud server.

---

## Activity 1: Create Test Files and Folder Structure

**Objective**: Prepare a sample directory for backup.

```powershell
New-Item -Path "C:\BackupLab\Documents\testfolder" -ItemType Directory -Force
1..5 | ForEach-Object { New-Item -Path "C:\BackupLab\Documents" -Name "file$_.txt" -ItemType File }
1..5 | ForEach-Object { New-Item -Path "C:\BackupLab\Documents\testfolder" -Name "file$_.txt" -ItemType File }
```

---

## Activity 2: Create a Basic PowerShell Script

**Objective**: Create a script to echo a message.

```powershell
New-Item -Path "C:\BackupLab\backupscript.ps1" -ItemType File -Force
Set-Content -Path "C:\BackupLab\backupscript.ps1" -Value 'Write-Output "Backup script initiated."'
```

---

## Activity 3: Add Timestamp Variable

**Objective**: Add a timestamp to the script.

```powershell
Add-Content -Path "C:\BackupLab\backupscript.ps1" -Value '$now = Get-Date -Format "dd_MM_yy"'
```

---

## Activity 4: Archive Files with `Compress-Archive`

**Objective**: Create zip backup of files.

```powershell
Add-Content -Path "C:\BackupLab\backupscript.ps1" -Value 'Compress-Archive -Path "C:\BackupLab\Documents\*" -DestinationPath "C:\BackupLab\backup_$now.zip" -Force'
```

---

## Activity 5: Rename Zip Files Using Variable

**Objective**: Show use of variables to rename files.

(This is handled during compression using `$now` variable.)

---

## Activity 6: Run Script and Validate

**Objective**: Test the script.

```powershell
powershell -ExecutionPolicy Bypass -File "C:\BackupLab\backupscript.ps1"
```

---

## Activity 7: Add to Environment Path (Optional)

**Objective**: Add script location to system path for global execution.

```powershell
# Optional: Add C:\BackupLab to PATH using Environment Variable settings
```

---

## Activity 8: Automate with Task Scheduler

**Objective**: Run script hourly.

1. Open Task Scheduler > Create Task
2. Name: `HourlyBackup`
3. Triggers > New > Begin task: On a schedule > Repeat every 1 hour
4. Actions > New > Program/script:

```text
powershell.exe
```

5. Add arguments:

```text
-ExecutionPolicy Bypass -File "C:\BackupLab\backupscript.ps1"
```

6. Apply and Test.

---

## Activity 9: Export Backup via `scp` on Windows

**Objective**: Use `scp` to send backup.

Install [WinSCP](https://winscp.net/) or OpenSSH client.

```powershell
scp -i C:\Users\You\.ssh\id_rsa "C:\BackupLab\backup_$now.zip" ubuntu@<remote-ip>:/home/ubuntu/
```

---

## Activity 10: SSH into Remote Server to Accept Key

**Objective**: Accept host fingerprint for automation.

```powershell
ssh -i C:\Users\You\.ssh\id_rsa ubuntu@<remote-ip>
```

Exit once connected.

---

## Activity 11: Schedule on Boot (Challenge)

**Objective**: Run backup at every system startup.

1. In Task Scheduler > Create Task
2. Trigger: At startup
3. Action: Same PowerShell script as above

---

## Activity 12: Customize Welcome Message (Challenge)

**Objective**: Display PowerShell ASCII welcome on start.

```powershell
Install-Module -Name PSASCIIArt -Scope CurrentUser
"Write-Output (Get-ASCIIArt 'Welcome')" | Add-Content -Path "$PROFILE"
```

---

## End of Lab

Validate that your PowerShell script creates timestamped backups hourly and exports them securely to a cloud server. Ensure your scheduled tasks work on schedule and at boot.


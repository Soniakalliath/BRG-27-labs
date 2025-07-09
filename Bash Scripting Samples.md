# Lab: Bash Backup Scripting, Cron Jobs & Cloud Export (Expanded to 12 Hands-On Activities)

## Objective

Learn how to automate system backups using Bash scripting and cron, and export backups to a remote cloud server securely.

---

## Activity 1: Create Test Files and Directory Structure

**Objective**: Prepare a sample directory for backup.

```bash
mkdir -p /home/ubuntu/Documents/testfolder
cd /home/ubuntu/Documents

touch file1 file2 file3 file4 file5
cd testfolder
touch file11 file22 file33 file44 file55
```

---

## Activity 2: Write a Basic Bash Script

**Objective**: Begin your backup script.

```bash
nano /home/ubuntu/testscript.sh
```

Add:

```bash
#!/bin/bash
echo "Backup script initiated."
```

---

## Activity 3: Use Variables and Date Formatting

**Objective**: Add timestamped filenames.

```bash
now=$(date +"%d_%m_%y")
echo "Today's date is $now"
```

---

## Activity 4: Archive Files with cp and zip

**Objective**: Perform backup of files and compress.

```bash
cp -R /home/ubuntu/Documents /home/ubuntu/backup/
zip -r "/home/ubuntu/$now.zip" /home/ubuntu/backup/
```

---

## Activity 5: Rename Files Dynamically

**Objective**: Show use of variables to rename files.

```bash
mv /home/ubuntu/backup.zip /home/ubuntu/backup_$now.zip
```

---

## Activity 6: Set Permissions and Test Script

**Objective**: Make script executable and run.

```bash
chmod +x /home/ubuntu/testscript.sh
./home/ubuntu/testscript.sh
```

---

## Activity 7: Move Script to System Path

**Objective**: Make your script globally executable.

```bash
sudo mv /home/ubuntu/testscript.sh /usr/bin/testscript
sudo chown ubuntu /usr/bin/testscript
```

Test it by running:

```bash
testscript
```

---

## Activity 8: Automate with Cron

**Objective**: Schedule script every hour.

```bash
sudo nano /etc/crontab
```

Add:

```text
0 * * * * ubuntu /usr/bin/testscript
```

---

## Activity 9: Use `scp` to Export to Cloud

**Objective**: Transfer backups to remote server.

```bash
scp -i ~/cloudkey.pem /home/ubuntu/$now.zip ubuntu@remote-ip:/home/ubuntu/
```

---

## Activity 10: SSH into Remote Server as Root

**Objective**: Accept host key so cron can scp.

```bash
sudo ssh -i ~/cloudkey.pem ubuntu@remote-ip
```

Then exit.

---

## Activity 11: Boot-Time Execution (Challenge)

**Objective**: Ensure script runs on boot.

```bash
sudo crontab -e
```

Add:

```text
@reboot /usr/bin/testscript
```

---

## Activity 12: Customize Terminal Greetings (Challenge)

**Objective**: Use figlet and neofetch.

```bash
sudo apt install figlet neofetch
```

Edit `.bashrc`:

```bash
echo "figlet Welcome" >> ~/.bashrc
echo "neofetch" >> ~/.bashrc
```

---

## End of Lab

Test and validate all components. Backup files should be created every hour and securely exported to the cloud server. Confirm cron and boot automation are working.


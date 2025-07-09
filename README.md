Bash & Server Automation Labs
Welcome to this hands-on repository built for anyone interested in learning Linux server automation, Apache management, DNS setup, HTTPS with Let's Encrypt, and useful scripting techniques in both Bash and PowerShell.

This collection of lab exercises, guides, and working scripts is ideal for students, DevOps beginners, and IT admins who want to sharpen their command-line and server configuration skills in real-world scenarios.

📂 What's Inside?
🧠 Core Learning Activities
🔁 Bash Scripting Samples.md
A step-by-step lab covering 12 activities that teach you how to:

Automate backups using Bash

Schedule jobs with cron

Transfer files securely to the cloud

Customize login greetings using tools like figlet and neofetch

A perfect starting point for anyone learning Bash scripting and cron-based automation.
→ Great for daily server management tasks.

🔒 HTTPS & DNS Configuration
🌐 Activity-dns-certbot.md
A full walkthrough on how to:

Register a domain

Link it to your cloud VM using DNS A records

Install Apache and Certbot

Enable HTTPS for your site using Let’s Encrypt

Includes verification, DNS tools like dig/nslookup, and certificate renewal steps.

🔐 Activity-letsencrypt-certbot.md
More focused on the Let's Encrypt certificate process:

Certbot installation using Snap

HTTPS setup and testing

Auto-renewal checks for SSL certs

Perfect for securing websites hosted on Ubuntu servers.

📜 Server Scripting Cheat Sheets
🐧 linux.md
A collection of Bash scripts for:

User/group management

Disk usage alerts and quotas

Service health checks

Backups, log cleaning, and scheduled jobs

Ideal for system admins who manage Linux servers.

🪟 windows.md
PowerShell-based tools for Windows Server:

Creating users/groups (even in bulk!)

Monitoring CPU, memory, and disk

Automating backups and daily tasks with Task Scheduler

Great reference if you work in mixed Linux/Windows environments.

🔍 Parsing and Analyzing Apache Logs
📄 ApacheLogs-user_agent.md
Extracts IP, HTTP method, URL, status code, and User-Agent from Apache logs.
Useful for understanding who's visiting your site and what browsers or devices they use.

🚨 ApacheLogs-failed_requests.md
Filters and displays only the failed HTTP requests (status 400 and above).
Great for monitoring and troubleshooting web server errors.

📊 2b-2 ApacheLogs-csv_output (1).md
Outputs parsed Apache logs in CSV format – ready for spreadsheet or data analysis.
Makes it easier to import into tools like Excel or Python.

🔧 Command-Line Mastery
🧮 awk_101_guide.md
A beginner-friendly guide to AWK, covering:

Text processing patterns

Summing columns

Skipping lines and working with fields

Ideal if you're processing logs or structured data on the command line.

🔤 regex_101_guide.md
Explains regular expressions in plain English with practical examples using:

grep, awk, sed

Email and IP address patterns

Special characters and boundaries

Must-have for debugging, parsing, or searching text efficiently.

💡 Who This Is For
Students learning Linux system administration or DevOps

Engineers setting up servers and securing domains

Anyone exploring scripting and automation in a hands-on way

✅ How to Use
Clone this repository.

Follow each markdown file like a lab guide.

Run scripts in your own Linux/Windows test environment (e.g., local VM or cloud).

Customize scripts to suit your setup or project.


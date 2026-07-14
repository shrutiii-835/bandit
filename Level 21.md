## Objective

The goal of this level was to find the password for Bandit Level 22.

In this level, a program was running automatically at regular intervals using the Linux `cron` job scheduler.

The challenge was to:

1. Understand that Linux can automatically execute commands using cron.
2. Find the cron configuration responsible for running the program.
3. Identify which command/script was being executed.
4. Inspect that script to understand what it was doing.
5. Locate the file where the password for the next level was stored.

The password was not directly accessible because it belonged to another user. However, the cron job was running with that user's privileges and was performing an action that exposed the password in another location.


## Commands Used

### 1. Listing cron configuration files

Command:

ls -l /etc/cron.d/

Purpose:

This command was used to view all system-level cron jobs configured on the machine.

The `/etc/cron.d/` directory contains cron configuration files that define commands which should be executed automatically at specific times.

The output showed cron files related to different Bandit levels.


### 2. Reading the cron job configuration

Command:

cat /etc/cron.d/cronjob_bandit22

Purpose:

This was used to inspect the cron configuration file for the next level.

The file showed which command was being executed automatically and which user was running it.

A cron entry looks like:

* * * * * username command

The five time fields define when the command runs, followed by the user who executes it and the command/script path.

Example:

* * * * * bandit22 /usr/bin/cronjob_bandit22.sh

This means:

- Run every minute.
- Execute the command as user `bandit22`.
- Run the script `/usr/bin/cronjob_bandit22.sh`.


### 3. Reading the script executed by cron

Command:

cat /usr/bin/cronjob_bandit22.sh

Purpose:

This command was used to inspect the script that cron was executing.

The script showed that it was accessing the password file belonging to the next user and copying the password into another location where it could be accessed.

The important part was identifying the destination file where the password was stored.


### 4. Reading the generated password file

Command:

cat /tmp/<password_file>

Purpose:

The cron script copied the password into a temporary file.

Since the file was created with permissions that allowed access, reading this file revealed the password for the next level.


## Why the Solution Worked

The main idea behind this level was understanding how automated tasks work in Linux using cron.

Normally, the current user (`bandit21`) cannot directly read the password file of another user:

cat /etc/bandit_pass/bandit22

would fail because of permission restrictions.

However, cron jobs can run commands as specific users.

The cron configuration contained:

bandit22 /path/to/script.sh

which means the script was executed with `bandit22` privileges.

The flow was:

1. Cron automatically executed the script at regular intervals.
2. The script ran as user `bandit22`.
3. Because it had `bandit22` permissions, it could access the bandit22 password file.
4. The script copied the password into another file.
5. That file could be read by the current user.
6. Reading that file provided the password for Bandit Level 22.

The important concept was that instead of directly attacking permissions, we used an already running automated process that had the required privileges.


## Linux Concepts / Commands Learned

### 1. Cron

Cron is a time-based job scheduler in Linux.

It allows the system to automatically execute commands or scripts at specific times or intervals.

Examples of tasks commonly handled by cron:

- Running backups every night.
- Cleaning temporary files regularly.
- Monitoring system health.
- Generating scheduled reports.

Instead of manually running commands, cron automates them.


### 2. Cron Jobs

A cron job is a scheduled command that cron executes automatically.

A cron job contains:

- Schedule information.
- User account that runs the command.
- The command or script to execute.

Example:

0 2 * * * user /home/user/backup.sh

Meaning:

Run `backup.sh` every day at 2 AM as `user`.


### 3. /etc/cron.d Directory

The `/etc/cron.d/` directory stores system-wide cron configurations.

Unlike user-specific cron jobs, these jobs are managed by administrators and can run commands as different users.

This level required checking this directory because the challenge stated that a program was running automatically from cron.


### 4. Understanding Cron Time Format

Cron uses five fields to define when a job runs:

Minute   Hour   Day of Month   Month   Day of Week

Example:

* * * * *

means:

Every minute,
Every hour,
Every day,
Every month,
Every day of the week.


### 5. File Permissions and User Privileges

Linux restricts access to files based on ownership and permissions.

A user normally cannot access another user's files.

However, processes running under another user's account can access resources available to that user.

In this level:

bandit22 cron job

↓

runs with bandit22 privileges

↓

accesses protected files

↓

stores the password somewhere accessible


### 6. Automation in Linux

Cron is one of the fundamental automation tools used in Linux administration and DevOps.

It is commonly used for:

- Automated backups.
- Log rotation.
- System monitoring.
- Database maintenance.
- Scheduled scripts.

Understanding cron is important when managing production servers because many background tasks depend on scheduled automation.


## Summary

This level introduced Linux job scheduling using cron.

Instead of manually running a command, Linux can automatically execute programs at scheduled intervals using cron jobs.

By inspecting `/etc/cron.d/`, identifying the correct cron configuration, reading the script being executed, and locating the file where the script stored the password, we were able to retrieve the password for the next level.

The major concepts learned were:

- Cron and cron jobs.
- System-level scheduled tasks.
- Reading cron configurations.
- Understanding user privileges.
- How automated processes can perform actions with different permissions.
# Bandit Level 19 → Level 20

# The objective -

* To find the password for **LEVEL20** by using the setuid program `bandit20-do` to execute a command with the permissions of the `bandit20` user.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls -l`
* `./bandit20-do id`
* `./bandit20-do cat /etc/bandit_pass/bandit20`

# Why your solution worked -

* After logging into the level, I listed the files in the home directory and found an executable named `bandit20-do`.
* I checked its permissions using `ls -l` and noticed that it had the **setuid (SUID)** permission enabled.
* To understand what the program did, I first ran:
  `./bandit20-do id`
* The output showed that although I was logged in as `bandit19`, the command was executed with the effective permissions of the `bandit20` user.
* Since the password for the next level was stored in `/etc/bandit_pass/bandit20`, I used the program to execute:
  `./bandit20-do cat /etc/bandit_pass/bandit20`
* The command displayed the password for **LEVEL20**.
* The solution worked because the SUID bit allows an executable to run with the permissions of its owner instead of the user executing it. Since `bandit20-do` is owned by `bandit20`, it was able to access files that `bandit19` could not read directly.

# Key Linux concepts or commands you learned -

* **SUID (Set User ID)** is a special file permission that allows an executable to run with the permissions of its owner.
* `ls -l` displays special permissions such as the `s` in place of the executable bit.
* The `id` command displays information about the current user's real and effective identities.
* Executables with the SUID bit can temporarily grant higher privileges to perform specific tasks.
* SUID programs are commonly used for legitimate administrative purposes, but if they are poorly designed, they can also become security vulnerabilities.
* Understanding file permissions and privilege escalation is essential for Linux system administration and cybersecurity.

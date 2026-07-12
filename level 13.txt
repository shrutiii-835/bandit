# Bandit Level 13 → Level 14

# The objective -

* To find the password for **LEVEL14** by using the **SSH private key** provided in the home directory to log in as the `bandit14` user.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls`
* `cat sshkey.private`
* `ls -l`
* `ssh -i sshkey.private bandit14@localhost -p 2220`
* `cat /etc/bandit_pass/bandit14`
* `exit`

# Why your solution worked -

* After logging into the level, I listed the files in the home directory and found a file named `sshkey.private`.
* I checked the file permissions using `ls -l` and confirmed that it was a private SSH key.
* Instead of using a password, I connected to the next user account by specifying the private key with the `-i` option:
  `ssh -i sshkey.private bandit14@localhost -p 2220`
* Since I was already on the Bandit server, I connected to `localhost`, which refers to the same machine.
* After successfully logging in as `bandit14`, I accessed the password stored in `/etc/bandit_pass/bandit14` using the `cat` command.
* The solution worked because SSH supports key-based authentication. The server verified the private key, allowing me to log in without entering a password. Once authenticated as `bandit14`, I had permission to read that user's password file.

# Key Linux concepts or commands you learned -

* SSH supports both **password-based** and **key-based** authentication.
* The `-i` option in the `ssh` command specifies the private key to use for authentication.
* `localhost` refers to the current machine (IP address `127.0.0.1`).
* Private SSH keys should be kept secure because they provide access without requiring a password.
* User passwords for the Bandit levels are stored in `/etc/bandit_pass/`, and only the corresponding user has permission to read their password file.
* `ls -l` displays file permissions and helps identify special files such as private keys.

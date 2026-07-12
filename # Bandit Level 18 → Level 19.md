# Bandit Level 18 → Level 19

# The objective -

* To find the password for **LEVEL19**. The password is stored in the file `readme` in the home directory, but the `.bashrc` file automatically logs the user out whenever an interactive shell is started.

# The commands you used -

* `ssh username@hostname -p <port>`
* `ssh username@hostname -p <port> cat readme`

# Why your solution worked -

* When I tried logging into the `bandit18` account normally, the session closed immediately after login.
* The challenge explained that the `.bashrc` file had been modified to log the user out whenever an interactive shell was started.
* Instead of opening an interactive shell, I executed a command directly during the SSH connection:
  `ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`
* SSH connected to the remote machine, executed the `cat readme` command immediately, displayed the contents of the file, and then closed the connection.
* Since no interactive shell was started, the commands inside `.bashrc` were never executed.
* The solution worked because SSH allows a command to be executed directly on the remote system without launching a login shell, bypassing the modified shell configuration.

# Key Linux concepts or commands you learned -

* SSH can execute a command directly on a remote machine without opening an interactive shell.
* The general syntax is:
  `ssh username@hostname -p <port> <command>`
* `.bashrc` is a shell initialization file that runs whenever an interactive Bash shell starts.
* If an interactive shell is not started, `.bashrc` is generally not executed.
* Executing remote commands through SSH is a common practice for system administration, automation, and deployment tasks because it avoids the need for an interactive session.

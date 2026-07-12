# Bandit Level 16 → Level 17

# The objective -

* To find the password for **LEVEL17** by discovering which port between **31000** and **32000** is running an **SSL/TLS service**, submitting the current level's password to that service, and retrieving the SSH private key for the next level.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `cat /etc/bandit_pass/bandit16`
* `nmap -sV localhost -p 31000-32000`
* `openssl s_client -connect localhost:<port>`
* *(paste the password and press Enter)*
* `mkdir /tmp/<your_directory>`
* `cd /tmp/<your_directory>`
* `nano sshkey.private`
* *(paste the private key and save the file)*
* `chmod 600 sshkey.private`
* `ssh -i sshkey.private bandit17@localhost -p 2220`

# Why your solution worked -

* After logging in as `bandit16`, I first read the current level's password from `/etc/bandit_pass/bandit16`.
* The challenge stated that the correct service was listening on a port between **31000** and **32000**, but it did not specify which one.
* I used `nmap` with service detection to scan all the ports in that range:
  `nmap -sV localhost -p 31000-32000`
* The scan identified a few open ports, but only one of them was running an SSL/TLS service that accepted the password and returned a valid response.
* I connected to that port using `openssl s_client`, entered the current level's password, and the server returned an SSH private key instead of the next password.
* I copied the private key into a file named `sshkey.private`, changed its permissions to `600` so that only my user could read and write it, and then used it to log in as `bandit17`.
* The solution worked because `nmap` helped identify the correct service, `openssl s_client` established a secure connection, and the private key provided authenticated access to the next user account.

# Key Linux concepts or commands you learned -

* `nmap` is a network scanning tool used to discover open ports and identify the services running on them.
* The `-sV` option performs service version detection, helping distinguish between different types of network services.
* `openssl s_client` is used to communicate with SSL/TLS-enabled services.
* SSH private keys must have secure permissions before they can be used for authentication.
* `chmod 600` allows only the file owner to read and write the private key, preventing access by other users.
* Port scanning is a common technique used by system administrators and security professionals to identify available services on a machine.

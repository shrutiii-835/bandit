# Bandit Level 14 → Level 15

# The objective -

* To find the password for **LEVEL15** by submitting the current level's password to a service listening on **localhost** at **port 30000**.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `cat /etc/bandit_pass/bandit14`
* `nc localhost 30000`
* *(paste the password and press Enter)*

# Why your solution worked -

* After logging in as `bandit14`, I first read the current level's password from `/etc/bandit_pass/bandit14`.
* The challenge instructed me to send this password to a service running on `localhost` at port `30000`.
* I used the `nc` (Netcat) command to establish a connection to the specified port:
  `nc localhost 30000`
* Once the connection was established, I pasted the password and pressed **Enter**.
* The service verified the password and responded with the password for **LEVEL15**.
* The solution worked because `nc` creates a TCP connection to the specified host and port, allowing me to communicate directly with the service. After receiving the correct password, the service returned the credentials for the next level.

# Key Linux concepts or commands you learned -

* `nc` (Netcat) is a networking utility used to create TCP or UDP connections.
* `localhost` refers to the current machine where the service is running.
* A **port** is a communication endpoint that allows different services to run on the same machine.
* Many applications communicate over the network by listening on specific ports.
* Netcat can be used to send and receive data, making it a useful tool for testing network services and troubleshooting connections.
* Services often validate input before returning a response, similar to how client-server applications communicate in real-world systems.

# Bandit Level 15 → Level 16

# The objective -

* To find the password for **LEVEL16** by submitting the current level's password to a service running on **localhost** at **port 30001** using an **SSL/TLS encrypted connection**.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `cat /etc/bandit_pass/bandit15`
* `openssl s_client -connect localhost:30001`
* *(paste the password and press Enter)*

# Why your solution worked -

* After logging in as `bandit15`, I first read the current level's password from `/etc/bandit_pass/bandit15`.
* The challenge specified that the service on port `30001` communicated over **SSL/TLS**, so using `nc` would not work because it does not establish an encrypted connection.
* I used the following command to connect securely:
  `openssl s_client -connect localhost:30001`
* The command performed the SSL/TLS handshake and successfully established a secure connection with the service.
* Once the connection was established, I pasted the current level's password and pressed **Enter**.
* The service verified the password and returned the password for **LEVEL16**.
* The solution worked because `openssl s_client` is designed to communicate with SSL/TLS-enabled services. It encrypted the communication between my client and the server, allowing the service to accept the request and respond with the next password.

# Key Linux concepts or commands you learned -

* Some network services require **SSL/TLS encryption** instead of a regular TCP connection.
* `openssl s_client` is used to establish and test secure SSL/TLS connections from the command line.
* The `-connect` option specifies the hostname and port of the remote service.
* SSL/TLS encrypts data exchanged between the client and the server, protecting it from interception.
* Using the correct protocol is just as important as connecting to the correct host and port. A service expecting encrypted communication will not respond correctly to a plain-text client like `nc`.
* OpenSSL is widely used for testing HTTPS servers, secure APIs, and encrypted network services in real-world environments.

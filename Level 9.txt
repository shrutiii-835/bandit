# Bandit Level 9 → Level 10

# The objective -

* To find the password for **LEVEL10** stored in one of the files in the home directory. The password is located in the **only human-readable string**, preceded by several `=` characters.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls`
* `file data.txt`
* `strings data.txt`
* `strings data.txt | grep "="`
* `strings data.txt | grep "===="`

# Why your solution worked -

* After logging into the level, I listed the files in the home directory and found a file named `data.txt`.
* Since the challenge mentioned that the password was hidden inside a binary file, I first checked its type using the `file` command. The output confirmed that it was not a regular text file.
* Reading the file directly with `cat` produced unreadable characters because binary files contain non-printable data.
* I then used the `strings` command, which extracts only the human-readable text from a binary file.
* The challenge also mentioned that the password was preceded by several `=` characters, so instead of manually searching through all the extracted text, I filtered the output using `grep`.
* Running `strings data.txt | grep "===="` displayed the line containing multiple `=` symbols followed by the password.
* The solution worked because `strings` ignored the binary content and extracted only readable text, while `grep` narrowed down the output to the line matching the required pattern.

# Key Linux concepts or commands you learned -

* Binary files cannot always be read using `cat` because they contain non-printable characters.
* The `file` command helps identify the type of a file before deciding how to inspect it.
* The `strings` command extracts readable text from binary files.
* `grep` is useful for filtering output based on a specific word or pattern.
* Commands can be combined using the pipe operator (`|`), where the output of one command becomes the input of another.
* Using command pipelines makes searching through large amounts of data much faster than inspecting everything manually.

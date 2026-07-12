# Bandit Level 17 → Level 18

# The objective -

* To find the password for **LEVEL18**. The password is stored in the file `passwords.new` and is the **only line that differs** from the contents of `passwords.old`.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls`
* `cat passwords.old`
* `cat passwords.new`
* `diff passwords.old passwords.new`

# Why your solution worked -

* After logging in as `bandit17`, I listed the files in the home directory and found two files: `passwords.old` and `passwords.new`.
* The challenge stated that the password was the only line that had changed between the two files.
* I could have opened both files individually, but comparing them manually would have been time-consuming and prone to mistakes.
* Instead, I used the `diff` command:
  `diff passwords.old passwords.new`
* The command compared both files line by line and displayed only the differences between them.
* From the output, I identified the line that appeared in `passwords.new` but not in `passwords.old`. That line was the password for **LEVEL18**.
* The solution worked because `diff` is designed to compare two files and report only the lines that have been added, removed, or modified, making it the fastest way to locate the changed password.

# Key Linux concepts or commands you learned -

* `diff` compares two files and highlights the differences between them.
* Using comparison tools is much more efficient than manually inspecting large files.
* The output of `diff` indicates which lines were changed, added, or removed between two files.
* Linux provides many utilities that simplify repetitive tasks, and choosing the right tool can save a significant amount of time.
* File comparison is commonly used in software development, version control, configuration management, and debugging to identify changes between different versions of a file.

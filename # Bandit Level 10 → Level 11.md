# Bandit Level 10 → Level 11

# The objective -

* To find the password for **LEVEL11**. The password is stored in the file `data.txt` and has been **Base64 encoded**.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls`
* `cat data.txt`
* `base64 -d data.txt`
* `cat data.txt | base64 -d`

# Why your solution worked -

* After logging into the level, I listed the files in the home directory and found a file named `data.txt`.
* I opened the file using `cat` and noticed that the contents were a long string containing uppercase and lowercase letters, numbers, and the `=` character at the end. This indicated that the text was likely Base64 encoded.
* Since the challenge explicitly mentioned that the password was Base64 encoded, I used the `base64` command with the `-d` option to decode the file.
* Running `base64 -d data.txt` converted the encoded text back into its original form and displayed the password for the next level.
* The solution worked because Base64 is an encoding scheme, not an encryption method. The `-d` option tells the `base64` command to decode the encoded data and recover the original text.

# Key Linux concepts or commands you learned -

* Base64 is an **encoding** technique used to represent binary or text data using printable ASCII characters.
* Encoded data can be converted back to its original form using `base64 -d`.
* The `=` character at the end of a Base64 string is used as padding to make the encoded output a multiple of four characters.
* Data encoding is different from encryption because encoded data can be decoded without requiring a secret key.
* The output of one command can be passed to another using a pipe (`|`), as in `cat data.txt | base64 -d`.

# Bandit Level 11 → Level 12

# The objective -

* To find the password for **LEVEL12**. The password is stored in the file `data.txt`, where all lowercase (`a-z`) and uppercase (`A-Z`) letters have been rotated by **13 positions (ROT13)**.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls`
* `cat data.txt`
* `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
* `tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt`

# Why your solution worked -

* After logging into the level, I listed the files in the home directory and found `data.txt`.
* I opened the file using `cat` and saw that the text was readable, but it did not make any sense. The challenge description mentioned that the contents were encoded using **ROT13**.
* ROT13 works by replacing each letter with the one that is 13 positions ahead in the alphabet. Applying the same transformation again converts the text back to its original form.
* I used the `tr` command to translate each uppercase and lowercase letter according to the ROT13 mapping:
  `tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt`
* The command decoded the text and displayed the password for the next level.
* The solution worked because `tr` performs character-by-character translation. By providing the correct source and destination character sets, every letter was shifted back to its original value, while numbers and special characters remained unchanged.

# Key Linux concepts or commands you learned -

* ROT13 is a simple letter substitution technique where each alphabet character is rotated by 13 positions.
* Applying ROT13 twice returns the original text because the transformation is symmetric.
* The `tr` command is used to translate or replace characters from one set with another.
* Input redirection (`<`) allows a command to read data directly from a file instead of standard input.
* Simple encoding techniques like ROT13 are useful for learning text manipulation, but they do not provide real security.

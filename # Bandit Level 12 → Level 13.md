# Bandit Level 12 → Level 13

# The objective -

* To find the password for **LEVEL13**. The password is hidden inside the file `data.txt`, which contains a **hex dump** of a file that has been compressed multiple times using different compression formats.

# The commands you used -

* `ssh username@hostname -p <port>`
* `pwd`
* `ls`
* `mkdir /tmp/<your_directory>`
* `cp data.txt /tmp/<your_directory>`
* `cd /tmp/<your_directory>`
* `xxd -r data.txt > data`
* `file data`
* `mv data data.gz`
* `gunzip data.gz`
* `file data`
* `mv data data.bz2`
* `bunzip2 data.bz2`
* `file data`
* `mv data data.gz`
* `gunzip data.gz`
* `file data`
* `mv data data.tar`
* `tar -xf data.tar`
* `file data5.bin`
* `mv data5.bin data.tar`
* `tar -xf data.tar`
* `file data6.bin`
* `mv data6.bin data.bz2`
* `bunzip2 data.bz2`
* `file data6`
* `mv data6 data.tar`
* `tar -xf data.tar`
* `file data8.bin`
* `mv data8.bin data.gz`
* `gunzip data.gz`
* `cat data8`

# Why your solution worked -

* After logging in, I found the file `data.txt` in the home directory. The challenge description mentioned that it contained a hex dump, so I first copied it to a temporary directory because I would need to modify the file during extraction.
* I used `xxd -r` to reverse the hex dump and recreate the original binary file.
* Since I did not know the file format, I repeatedly used the `file` command to identify what type of compressed file I had after each extraction.
* Depending on the output of the `file` command, I renamed the file with the correct extension and used the appropriate extraction command:

  * `gunzip` for Gzip files
  * `bunzip2` for Bzip2 files
  * `tar -xf` for Tar archives
* Every time I extracted one layer, I checked the resulting file again using `file` because the next layer was compressed using a different format.
* I repeated this process several times until the final extracted file contained plain text.
* Finally, I opened the last file using `cat` and obtained the password for the next level.
* The solution worked because the `file` command correctly identified each compression format, allowing me to use the appropriate tool to remove one layer at a time until the original text file was revealed.

# Key Linux concepts or commands you learned -

* `xxd -r` reverses a hexadecimal dump and recreates the original binary file.
* The `file` command is extremely useful for identifying unknown file formats.
* `gunzip` extracts files compressed using the Gzip format.
* `bunzip2` extracts files compressed using the Bzip2 format.
* `tar -xf` extracts the contents of a Tar archive.
* Temporary directories under `/tmp` are useful for working with files that need to be modified.
* Some files can be compressed multiple times using different formats, requiring several rounds of extraction before reaching the actual content.
* A systematic approach of identifying the file type after every extraction is much more reliable than guessing the next command.

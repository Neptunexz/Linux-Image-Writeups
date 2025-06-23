# Forensic Questions

Forensic Question 1:

  * Forensic Question 1 asks the user to find a hidden message within a file located on their desktop. This question helps to teach components of files, and commands to retrieve the hidden information.

  * To find the hidden message, we need to think about ways data can be hidden in files. One such instance is by using getfattr to find the extended attributes of a file. If you run the sudo getfattr -d <file> command, you will find that the hidden message is "Yahaha! you found me!".

Forensic Question 2:

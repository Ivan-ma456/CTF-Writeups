# Challenge Information:
**Challenge Name:** Lost Luggage

**Category:** Cryptography

# Challenge Description:
I need to get into this archive, but I forgot the password for it as well. All I remember is, it's the same 4-digit pin I used on my luggage lock...

Archive Download Link: https://metaproblems.com/d36b89698928224c03f29aa2d2cb5544/luggage.zip

# Analysis:
The file flag.txt in the provided zip file is protected by a password, so we are unable to obtain the flag without the password. The challenge description suggests that the password is 4 digits long, so it can easily be brute-forced in seconds using a password cracking tool like John the Ripper. But first, we need to know the password hash. Running the command `./zip2john.exe luggage.zip > luggage.hashes` in a bash terminal takes the hash of the password protecting luggage.zip and writes it to the file luggage.hashes. You can run the command `cat luggage.hashes` to view the hash, which gives the following output:
```
luggage.zip/flag.txt:$pkzip2$1*1*2*0*44*38*f38c1c63*0*26*0*44*f38c*44ca*2481b39442623e50e6d5dcfd4d0ab924e93dbfc2c936731afc975888ade41050d368ee4d939a0f48131a11c41fa7982d6f71ac8f35d8c7edb0ba71b1dcca5356c9f7eae4*$/pkzip2$:flag.txt:luggage.zip::luggage.zip
```
From here, I ran the command `./john.exe luggage.hashes`, which gives the password 7123, which we can use to extract the zip file and obtain the flag from flag.txt.

**flag:** `MetaCTF{w0w_stup1d35t_c0mbin4t10n_1v3_he4rd_in_my_l1f3}`

# Lesson Learned:
- Learned how to use the zip2john tool to extract password hashes from password-protected files
- Learned how to use John the Ripper to crack a password hash
- Short, predictable, and common passwords can be cracked by tools like John the Ripper or Hashcat in seconds; it is good practice to refrain from using predictable short passwords to prevent breaches

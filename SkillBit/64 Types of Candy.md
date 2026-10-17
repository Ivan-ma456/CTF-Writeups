# Challenge Information:
**Challenge Name:** 64 Types of Candy

**Category:** Cryptography

# Challenge Description:
I asked my friend what type of candy they want to get to hand out tomorrow night, but they refuse to answer without using this weird cipher! Everytime I ask they respond with `TWV0YUNURntsMzdzX2cwX3cxdGhfZDRya19jaDBjMGw0dDN9`

# Analysis:
The ciphertext has only alphanumeric characters, and the title has 64 in it. This suggests trying to use base64 decoding on it, which gives the flag. One way to decode from base64 is to use the bash terminal command `echo 'TWV0YUNURntsMzdzX2cwX3cxdGhfZDRya19jaDBjMGw0dDN9' | base64 -d`. Another way is to use a tool like CyberChef or dCode.

**flag:** `MetaCTF{l37s_g0_w1th_d4rk_ch0c0l4t3}`

# Lesson Learned:
- Learned how to recognize base 64 ciphers
- Learned to use terminal commands as well as external tools to decode base64 ciphers

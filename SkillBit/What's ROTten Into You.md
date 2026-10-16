# Challenge Information:
**Challenge Name:** What's ROTten Into You?

**Category:** Cryptography

# Challenge Description:
I encrypted the flag with a very secure encryption method, windows even still uses it! `ZrgnPGS{jul_q03f_j1aq0jf_5gv11_h53_e0g13}`

# Analysis:
There are two ways to approach the challenge. The first one is to notice that ROT is specially capitalized in the challenge name, and that the description notes how Windows uses the encryption method used to encrypt the flag. These details point towards a ROT13 cipher, and applying it to the cipher gives the flag. Tools like CyberChef and dCode can be used to automatically apply the ROT13 cipher.

The second approach is to recognize that the cipher retains the format of many SkillBit flags, which is MetaCTF{...}. The cipher has a capital letter, three lowercase letters, then three more capital letters, then text inside curly brackets. When mapping Z to M, r to e, g to t, n to a, P to C, G to T, and S to F, I noticed that all of these mappings are 13-letter shifts, and applying the same 13-letter shift to all other letters in the cipher and retaining the digits gives the flag.

**flag:** `MetaCTF{why_d03s_w1nd0ws_5ti11_u53_r0t13}`

# Lesson Learned:
- Learned how to decode ROT13 ciphertexts and Caesar ciphers in general
- Learned how to recognize a Caesar cipher
- Windows still uses ROT13 for moderate obfuscation, even though it is easy to decode

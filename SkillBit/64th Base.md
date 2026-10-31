# Challenge Information:
**Challenge Name:** 64th Base

**Category:** Cryptography

# Challenge Description:
I'm workshopping a new baseball variant with 64 bases instead of 4, but all my players have been just exchanging messages like this instead of playing the game normally, can you figure out what they're saying?

`TWV0YUNURntoMHAzX3kwdV9nM3RfNF9oMG0zX3J1bn0=`

# Analysis:
As with many cryptography challenges, the challenge description and title give hints as to the intended decoding method. In this case, the mention of 64 bases in the challenge description and players exchanging messages in ciphers suggests the cipher is encoded in base 64. Each character in a base 64 cipher is represented by 6 bits. A common method to decode base 64 is to convert all of the characters to binary and group them into bytes, giving ASCII codes that can be converted to plain text. In this challenge, this does indeed leads to the flag.

**flag:** `SkillBit{0ct0pu5_m0r3_l1k3_0c7alpu5}`

# Lesson Learned:
- Challenge titles and descriptions often contain hints toward the intended encoding scheme
- Base64 encodes data using a 64-character alphabet, and each character is represented by 6 bits
- Recognizing common encodings can allow ciphertexts to be decoded almost immediately without deeper analysis

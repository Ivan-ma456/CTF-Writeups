# Challenge Information:
**Challenge Name:** Floating

**Category:** Cryptography

# Challenge Description:
Did you know that almost anything can be represented in IEEE754 floating point values?

240600592 212.2753143310547 2.7884192016691608e+23 5.623021054185822e+31 17611451687157891000 8.927742989328635e-10 16391240070931153000 5.639361688736244e-8 2.115975377137147e-7

# Analysis:
Based on the challenge description, we know that the floating point values conform by the IEEE754 standard. The two most common IEEE754 formats are float32 and float64. In float32, each value is represented by 32 bits: 1 for the sign, 8 for the exponent, and 23 for the mantissa. In float64, it is 64 bits: 1 for the sign, 11 for the exponent, and 52 for the mantissa. If the values are in float32, then the 9 floats gives 36 bytes of data, which can represent 36 characters, enough for a flag. Ultimately, IEEE754 values are still forms of binary data, so it is possible to reinterpret the bit patterns and groupings as raw bytes instead of numerical values. So the first plan is to convert to hexadecimal to extract the bytes and convert it from ASCII codes to plain text. In order, the 9 float values turn into the following hexadecimal values: `4d657461, 4354467b, 666c3034, 74316e67, 5f746872, 30756768, 5f637962, 33723570, 3463337d`. Extracting the bytes gives `4d 65 74 61 43 54 46 7b 66 6c 30 34 74 31 6e 67 5f 74 68 72 30 75 67 68 5f 63 79 62 33 72 35 70 34 63 33 7d`. Interpreting each of these as ASCII codes, converting to plain text, and concatenating them together gives the flag `MetaCTF{fl04t1ng_thr0ugh_cyb3r5p4c3}`.

**flag:** `MetaCTF{fl04t1ng_thr0ugh_cyb3r5p4c3}`

# Lesson Learned:
- IEEE754 floating-point values can be reinterpreted as raw binary data.
- The underlying bit patterns of float32 values can store arbitrary ASCII text.
- Comparing the expected plaintext length against the number of encoded values can help identify the correct data format.

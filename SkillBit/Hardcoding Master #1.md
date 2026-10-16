# Challenge Information:
**Challenge Name:** Hardcoding Master #1

**Category:** Reverse Engineering

# Challenge Description:
Storing secrets in applications securely is hard. As long as it's obfuscated, it's secure, right? Can you figure out the correct password for this program?

Program:
`def check_login(passcode):
    passcode = [ord(i) for i in passcode]
    hidden = [77,101,116,97,67,84,70,123,108,105,118,105,110,103,95,119,105,116,104,95,116,104,101,95,115,110,97,107,101,125]
    if len(passcode) != len(hidden):
        return False
    for i in range(len(hidden)):
        if hidden[i] != passcode[i]: return False
    return True

print("Login successful!" if check_login(input("Enter the password: ")) else "Login failed!")`

# Analysis:
The given program is a password checker. It takes each letter in the password you input, converts each character to its ASCII code using ord(i), and stores it in a list, retaining the order in which the characters appear in the password you input. If the resulting list matches a preset hidden password element for element, then you have the correct password. One approach to this problem would be to simply take a ASCII code table and convert each of the ASCII codes in hidden to characters (77 turns to M, 101 turns to e, etc.). Concatenate all of the resulting characters together, and you obtain the flag `MetaCTF{living_with_the_snake}`. This approach works fine for relatively short codes but would be impractical for something very long. An alternative solution would be to write a program that takes a list of ASCII codes, uses Python's built-in chr(i) method to recover the correct characters, and concatenates them all together. An example of this is given below.

`def recover_password(ASCII_list):
    characters = [chr(i) for i in ASCII_list]
    return ''.join(characters)
`

# Lesson Learned:
- Learned to reverse engineer a password stored via a list of ASCII codes
- Learned to recognize ASCII patterns
- ord(i) and chr(i) are inverse methods and can be used to help automate decoding text encoded via ASCII
- Sensitive information should not be hard-coded into public code

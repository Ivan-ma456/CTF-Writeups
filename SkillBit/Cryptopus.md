# Challenge Information:
**Challenge Name:** Cryptopus

**Category:** Cryptography

# Challenge Description:
I've spent years trying to communicate with non-human intelligence, and I've made a breakthrough! I can finally communicate numbers with octopi! Unfortunately, I can't figure out what they mean...

`123 153 151 154 154 102 151 164 173 60 143 164 60 160 165 65 137 155 60 162 63 137 154 61 153 63 137 60 143 67 141 154 160 165 65 175`

# Analysis:
The challenge description mentioning communicating with octopi highly suggests that the given cipher is in octal. Converting the octal numbers to base 10 numbers gives `83 107 105 108 108 66 105 116 123 48 99 116 48 112 117 53 95 109 48 114 51 95 108 49 107 51 95 48 99 55 97 108 112 117 53 125`. I noticed that most of these numbers fall within the range for ASCII codes for alphanumeric characters, so I mapped each number to their corresponding character and concatenated them together. Doing this for the first few ASCII codes already gave the characters `SkillBit{`, which highly suggested I was on the right track. Continuing this with the rest of the codes gave the flag. For codes of this length, it is possible to do all of the conversions by hand, but this would be infeasible for longer ciphers, so tools like CyberChef can be very useful here.

**flag:** `SkillBit{0ct0pu5_m0r3_l1k3_0c7alpu5}`

# Lesson Learned:
- Gained more familiarity in how challenge descriptions often hint toward intended encoding/decoding methods
- Learned how to convert octal numbers to decimal numbers
- Honed recognition for common ASCII codes and common flag prefixes/formatting

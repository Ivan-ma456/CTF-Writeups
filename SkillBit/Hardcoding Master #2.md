# Challenge Information:
**Challenge Name:** Hardcoding Master #2

**Category:** Reverse Engineering

# Challenge Description:
Here's another authentication module with a hard-coded password. Can you find the password this time?

Link: `https://metaproblems.com/06374b434081a1f16aa87e954555db50/hardcoding2.py`

Link Contents:

```
import random
a = input("Enter password: "); a += chr(random.randint(97,122))*(len(a)%2)
b = lambda a: "".join([a[b+1]+a[b] for b in range(0,len(a),2)])[::-1]
c = lambda b: "".join([chr(ord(b[c])+(-1)**(c+1)) for c in range(len(b))])[::-1]
print("Correct! Your flag is %s." % a if c(b(a))=="nhpouqb^umhhbqjuzs" else "Wrong... Try again.")
```

# Analysis:
The first step I took was to understand what the given code does. It imports random, then there are three variables `a`, `b`, and `c` initialized, and lastly, there is a print statement that prints the flag if you are able to find an input a that produces `"nhpouqb^umhhbqjuzs"` when performing `c(b(a))` but otherwise prints a message saying the password is invalid. The variable `a` is supposed to be a user-input password. Notably, the line `a += chr(random.randint(97, 122))*(len(a)%2)` means that `a` must have an even number of characters. If the user inputs a password with odd length, `len(a)%2` will be 1, so an extra lowercase character gets appended to the end of `a`. However, if the length of the password is even, then `len(a)%2` is 0, so nothing will be appended to `a`. Importantly, the operations performed to get `b` and `c` don't change the length of `a`, and the `c(b(a))` we are trying to reverse engineer has even length, so in this scenario, there is no need to worry about any randomness in this challenge. Next is understanding `b`. `b` takes a lambda variable `a` (not necessarily the same as the one from the previous line) and performs operations on it. Notice that the parameter in the `"".join()` method is a list comprehension that concatenates `a[b+1]` and `a[b]` for indices starting from 0 until `len(a)`, not including `len(a)` itself, and skipping every other index. This list comprehension thus produces a list of characters containing the same characters in `a`, except the first and second characters are swapped, the third and fourth characters are swapped, and so on. Finally, the characters in the list are concatenated together via the `"".join()` method and then reversed by the `[::-1]` at the end. For example, if `a = "hellothere"` then `b(a) = "reheotllhe"`. Finally, `c` also takes a lambda variable `b` (again, not necessarily the same as `b` from the previous line) and also consists of a `"".join()` method which has a list comprehension as its parameter. In `c`, the list comprehension takes a character in `b` and replaces it with the character with an ASCII code one more or one less than that character from `b` depending on the index of the character. Then, the characters are concatenated together and reversed. Continuing from the previous example where we ended up with `b(a) = "reheotlle"`, we will have `c(b(a)) = "dmkunfgfq"`. Now, we just need to find a way to find `a` such that `c(b(a))=="nhpouqb^umhhbqjuzs"` produces true. 

Just looking at the previous examples, it may be hard to discern a particular pattern for what `c(b(a))` results in and how to reverse engineer a password that gives the desired result. Thus, I examined the effect of `(c(b(a))` on a generic password with even length `a = a(1) a(2) a(3) ... a(2n)`, where `a(i)` is an arbitrary character in the English alphabet and all `a(i)` are concatenated together, a pattern actually does emerge. Performing `c(b(a))` gives `a''(2) a'(1) a''(4) a'(3) ... a''(2n) a'(2n-1)`, where `a''(i)` is the character with ASCII value one more than `a(i)` and `a'(i)` denotes the character that has ASCII value one less than `a(i)`. Thus, to recover `a` that gives the desired result, I wrote a program in Python that takes the characters in `c(b(a))` in pairs and undoes the character shifting to recover `a`. Here is the code:

```
def reverse(password):
    res = ""
    for i in range(0, len(password), 2):
        res += chr(ord(password[i + 1]) + 1) + chr(ord(password[i]) - 1)
    return res
```
Inputting `"nhpouqb^umhhbqjuzs"` as the password gives us the flag `import_antigravity`

**flag:** `import_antigravity`

# Lesson Learned:
- Breaking a complex transformation into smaller pieces makes reverse engineering much more manageable
- Writing out the effect of a program on a generic input can reveal patterns that are not obvious from test cases alone
- Once the forward transformation is understood, constructing the inverse transformation is often the fastest way to recover hidden inputs

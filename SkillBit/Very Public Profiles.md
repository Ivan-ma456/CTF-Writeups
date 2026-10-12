# Challenge Information:
**Challenge Name:** Very Public Profiles

**Category:** Web Exploitation

# Challenge Description:
ICMP Industries' website has a nice feature that allows you to view your profile, just by going to the website. In fact, you can see your profile by visiting below:

https://range.metaproblems.com/dc3bdd8c0d0d2fd9ae0edc87bc2d7674/icmpwebsite/profile/13/

Taking a closer look at the URL though, it almost seems as if you might can see other people's profiles...

# Analysis:
The challenge description hints at leveraging the given URL and its format to view other people's profiles. I noticed that the link ends in "/profile/13/" which suggested that profile identifiers were sequential. This prompted me to try changing the number, which indeed allowed me to view other profiles other than profile 13. Upon reaching profile 6, I found the flag. 

**flag:** `you_are_now_a_1337_url_h4x0r`

# Lesson Learned:
- Small changes to URL parameters can reveal sensitive information
- Sequential identifiers can allow unauthorized access to sensitive information without proper access control

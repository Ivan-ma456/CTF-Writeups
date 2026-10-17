# Challenge Information:
**Challenge Name:** Snowfall Wishes

**Category:** Web Exploitation

# Challenge Description:
Can you check out our cool new wishing website we're offering as an elf benefit? Maybe one day you'll even get access to our VIP wish package...

Access the website here: https://cyberlabhost.com/740df70f80b4f71f937cb582f7b978dd/

# Analysis:
In this web exploitation challenge, the provided website has a make-a-wish feature as well as a VIP wishing portal. I began by interacting with the buttons while monitoring incoming network traffic, but no additional requests were generated after the initial page loading, which meant most of the interaction logic ran client-side. But this meant that the VIP code validation was happeing locally, so I next looked at the page sources to see if there was any hidden data regarding the VIP wish portal or if I could directly extract a flag from the sources. After scrolling through, I eventually discovered the following block of code:

```
        // ============================================
        // VIP Access System
        // TODO: Move this check to the backend before launch!
        // For now the code is: frosty_flakes_2024
        // ============================================

        const _0xg1ft = "TWV0YUNURntjMGxkX2g0bmRzX3c0cm1faDM0cnRzX3N0MHBfcHU3NzFuZ19zM25zaTdpdmVfMW5mMF8xbl83aDNfY2xpM250X2gzNHJ0aH0=";

        function checkVIPAccess() {
            const codeInput = document.getElementById('vipCode');
            const messageDiv = document.getElementById('vipMessage');
            const enteredCode = codeInput.value;

            // Super secret VIP passphrase
            const secretCode = "frosty_flakes_2024";

            if (enteredCode === secretCode) {
                // Decode the gift for verified VIP members
                const decodedGift = atob(_0xg1ft);
                messageDiv.className = 'vip-message unlocked';
                messageDiv.innerHTML = `
                    <h4>🎉 VIP Access Granted! 🎉</h4>
                    <p>Welcome to the inner circle. Here's your special gift:</p>
                    <div class="flag">${decodedGift}</div>
                `;
            } else {
                messageDiv.className = 'vip-message unlocked';
                messageDiv.style.background = 'rgba(255, 100, 100, 0.1)';
                messageDiv.style.borderColor = 'rgba(255, 100, 100, 0.3)';
                messageDiv.innerHTML = `
                    <p style="color: #ff9999;">❌ Invalid VIP code. Nice try though!</p>
                `;
            }
        }
```

This is clearly out of place, and upon entering the code `frosty_flakes_2024` into the VIP wish portal, I recovered the flag `MetaCTF{c0ld_h4nds_w4rm_h34rts_st0p_pu771ng_s3nsi7ive_1nf0_1n_7h3_cli3nt_h34rth}`. An alternative way to recover the flag would be to decode the gift directly instead of entering the secret code. Based on the format of the gift, which contains alphanumeric characters and an equals sign at the end, I decided to try decoding it from base64, which gave the flag as well. Tools like CyberChef and dCode, as well as the terminal command `echo "TWV0YUNURntjMGxkX2g0bmRzX3c0cm1faDM0cnRzX3N0MHBfcHU3NzFuZ19zM25zaTdpdmVfMW5mMF8xbl83aDNfY2xpM250X2gzNHJ0aH0=" | base64 -d` all work to decode the flag.

**flag:** `MetaCTF{c0ld_h4nds_w4rm_h34rts_st0p_pu771ng_s3nsi7ive_1nf0_1n_7h3_cli3nt_h34rth}`

# Lesson Learned:
- Learned how to access and read through publicly available webpage sources to recover information that was unintentionally exposed through source-code
- Practiced using terminal commands as well as external tools to decode base64 ciphers

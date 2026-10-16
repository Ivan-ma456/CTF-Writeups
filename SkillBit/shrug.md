# Challenge Information:
**Challenge Name:** `¯\_(ツ)_/¯`

**Category:** Cryptography

# Challenge Description:
Plaintext: Lorem ipsum has et perpetua expetendis, explicari similique mnesarchum ei sed. Ius id tale persius assueverit. Sed vide autem erant te, justo fabellas an sit, et per sonet decore. Cum ad doctus placerat, sed at elit sensibus.
Adhuc animal adversarium sed ei. Ea vel partem noluisse interpretaris, ei iudico oratio temporibus per. Commodo eloquentiam vis eu, ne fierent dissentiet pri. Idque dolorum efficiendi eum ad, ut wisi nemore urbanitas eos. Eu eam inermis vituperatoribus possim, in vis graeci invidunt apeirian.


Ciphertext: Nwglq zhslq muf gb elvgwtle jrcgbtuhzk, eotqcpczx zmdalzuzy zpmhhvtzud in mrf. Qjz mu laci uyeuqjz ejkuvzjlvv. Atk zzve ryyyz gzpux kw, jlwyi scjtsprk ae wnn, rv xty wffek hjwbtm. Rbq rv dfgyof rtpjiist, jii ug gtxa wvfszfzm.
Nfpjj eeamrp fxigzhhvzmm jii yv. Gi klp gsrkir hbncxzwv ankiwjegbpymj, wi zyicpq wghxzg tvquiekjjz tvj. Cfqriqq mavulwnkmfg ika tb, rv xivvjhg fqhzielivx ulv. Klfbi uglfvzg rhnxjmvfdz izg nf, ci dmja nvqtlr wzqhrzlaj itm. Rw mpt mewrdmx pvvcelvrloimgof rwhzmd, an mmx aecmrp meniuysn nrmxymrf.

- The flag is the decoding key *

# Analysis:
I noticed that going from the plain text to cipher text did not change the character set of the text. Both the plaintext and ciphertext consist only of English alphabet. The spaces and word lengths are all preserved. Additionally, the given hint points at a key, so I realized that there was a high chance of this being a Vigenere cipher. Mapping 'L' to 'N' requires shifting forward 2 letters. Mapping 'o' to 'w' requires shifting forward by 8 letters. Continuing this process, we eventually see that there is a repeating pattern starting at the 14-th letter, suggesting a 14-character key. Converting each shift value into characters using the convention A=0, B=1, C=2, ..., Z=25, then we recover the key `CIPHERSAREFUN`, which is indeed the flag.

**flag:** `CIPHERSAREFUN`

# Lesson Learned:
- Learned to identify and decode Vigenere ciphers via characteristics such as preserved formatting
- Vigenere ciphers are not good for encoding text longer than the key due to repeating patterns, which enables frequency analysis

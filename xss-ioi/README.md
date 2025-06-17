# Discovery and responsible disclosure of a vulnerability (Reflected XSS) on the IOI Registration portal

![Screenshot 2025-06-17 at 00 48 57](https://github.com/user-attachments/assets/fe383623-7db3-4fe1-80d5-2edfea2bfe44)

While preparing for the British Informatics Olympiad, I discovered a critical Cross-site scripting (XSS) vulnerability on the official IOI registration portal:
- https://registration.ioinformatics.org 

## How I discovered it:
- I had pressed the "Passkey" button without selecting a passkey
- A message came up which said "Passkey did not work."
- I noticed this same text was visible in the url within the "message" parameter
- I then replaced replaced the word "work" with "1", which confirmed that the message parameter was indeed reflective
- I then inserted a script tag instead <script>alert(1)</script>, where the javascript executed; which confirmed that the parameter was unsanitised
- I tested redirects, cookie logging, and exfiltration to a temporary webhook; all had worked

## Vulnerability Details include:
- Unsanitised HTML reflection
- Injecting abstract javascript code was possible
- Cookie logging & exfiltration
- On the parameter "message"
- Full redirection to external domains

## Responsible Disclosure
Upon discovery, I immediately reported the issue to BIO.
As of writing (a day after it's discovery), the vulnerability has been silently patched, where the payloads are now properly escaped.

## Notes/Lessons Learned:
- Such commonly known issues such as XSS can exist even on high-profile, international platforms.
- The importance of penetration testing, if this issue had gone undiagnosed, a bad actor could have certainly taken far more malicious initiative

This vulnerability was reported in good faith for security improvement purposes only. No user data was accessed, stored, or exploited.

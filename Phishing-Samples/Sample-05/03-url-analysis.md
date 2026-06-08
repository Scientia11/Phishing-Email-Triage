Extracted URL 

```
https://tiktok.com/link/v2?aid=1180&lang=en&scene=bio_url&target=https://bit.ly/3s9UpOq

```
## Annalysis
1. The link does not point directly to the final destination.
Instead, it consists of a multi-stage redirect chain, directing the user through TikTok's redirect service,
TikTok then redirects to a Bitly, and Bitly redirects to the final destination.
This is a common tactic used by phishing actors to obscure the true destination.

2. Use of URL Shortener: The parameter "target=https://bit.ly/3s9UpOq" contains a Bitly link.
Attackers frequently use URL shorteners to hide the final domain and bypass simple email filters.
Prevent users from seeing the real destination, making phishing links appear less suspicious.

3. The email claims to be from Mashreq Bank, but the link involves TikTok and Bitly domains, neither of which is directly related to banking operations.

4. Flagged by two security vendors as malicious

5. The email appears to be coming from Mashreq, a bank in the Middle East(UAE), but the source IP 67.199.248.10 of the URL is located in the United States

---
title: "DNSSEC Deciphered"
date: 2022-06-26
---

After disabling DNSSEC and waiting for 48 hours, I realised that the DS record was still active. With an active DS record, I could not disable DNSSEC.

I thus attempted to find ways to remove the DS record. I discovered that by changing my DNS provider from Cloud DNS to Google Domains, I could unsign my domain using the Google Domains interface.

![]({{ site.baseurl }}/images/blog/2022-06-26-dns.png)

I don’t have a screenshot of the Google Domain’s interface but i promise the option is there. After un-signing my domain, the DS record was no longer being returned. And my website was finally loading correctly.

I was also able to successfully register Let’s encrypt certificate. Impressive.

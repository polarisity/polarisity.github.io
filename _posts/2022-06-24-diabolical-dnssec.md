---
title: "Diabolical DNSSEC"
date: 2022-06-24
---

In my [previous post]({% post_url /_posts/2022-06-23-setting-up-domain-with-gcp %}), we identified issues related to DNSSEC.

Google’s documentation explains it well [here](https://cloud.google.com/dns/docs/dnssec). Essentially it authenticates responses to domain name lookups so that these responses cannot be spoofed by other servers.

Because its a hassle to configure and use, i’ve decided to do away with it. However, I have found out how I can identify if my DNS is still configured with DNSSEC. It takes roughly 24 hours for configurations to propagate in GCP, so this helps me get an idea of when its ready.

The easiest way would be to use the [dig tool](https://toolbox.googleapps.com/apps/dig/#DS/). We should be able to identify the presence of DNSSEC by looking at the DS parameter. [This guide](https://servebolt.com/help/article/how-to-migrate-name-servers-for-dns-zones-with-dnssec-active/) provides more details.

![]({{ site.baseurl }}/images/blog/2022-06-24-gdig.png)

Not immediately intuitive, but I imagine an experienced professional would’ve been able to resolve this in a heartbeat. Now I’ll have to wait for my configurations to propagate.

![]({{ site.baseurl }}/images/blog/2022-06-24-deactivate-dnssec.png)

[Set up DNSSEC Security](https://support.google.com/domains/answer/6387342?hl=en#zippy=%2Cif-you-use-google-domains-name-servers)
{: .caption}

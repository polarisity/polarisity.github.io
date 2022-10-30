---
title: "Setting up a domain with GCP"
date: 2022-06-23
---

I decided to set up a domain name for this site. [This guide](https://cloud.google.com/dns/docs/tutorials/create-domain-tutorial) was helpful, but I’ve noticed slight quirks, which I will attempt to elaborate here.

I purchased a domain on Cloud Domains. Following which I had to link my domain on Cloud DNS. This image explains domains pretty well:

![]({{ site.baseurl }}/images/blog/2022-06-23-how-domain-work.png)

[wpbeginner](https://www.wpbeginner.com/beginners-guide/beginners-guide-what-is-a-domain-name-and-how-do-domains-work/)
{: .caption}

I did not realise that domains took a while to register. In fact, after a day, I am still unable to access it via my home ISP, and I’m only able to access it through my mobile carrier.

I’ve also encountered another problem. Apparently this is a [DNSSEC issue](https://community.letsencrypt.org/t/dns-problem-servfail-looking-up-a-for-mysite-the-domains-nameservers-may-be-malfunctioning-renew-cert/132575), which I’ve enabled (despite being explicitly told not to in the guide). [This site](https://check-your-website.server-daten.de/?q=oceanlion.org), [this site](https://dnsviz.net/d/oceanlion.org/dnssec/) and [this site](https://letsdebug.net/oceanlion.org/1088163) provide some interesting details which help in debugging DNS issues. Setting this up allows me to register an SSL certificate, which validates my website and stops browsers from giving me security issues.

```shell
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator webroot, Installer None
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for oceanlion.org
http-01 challenge for www.oceanlion.org
Using the webroot path /var/www/html for all unmatched domains.
Waiting for verification...
Challenge failed for domain oceanlion.org
Challenge failed for domain www.oceanlion.org
http-01 challenge for oceanlion.org
http-01 challenge for www.oceanlion.org
Cleaning up challenges
Some challenges have failed.

IMPORTANT NOTES:
 - The following errors were reported by the server:

   Domain: oceanlion.org
   Type:   dns
   Detail: DNS problem: SERVFAIL looking up A for oceanlion.org - the
   domain's nameservers may be malfunctioning; DNS problem: SERVFAIL
   looking up AAAA for oceanlion.org - the domain's nameservers may be
   malfunctioning

   Domain: www.oceanlion.org
   Type:   dns
   Detail: DNS problem: SERVFAIL looking up A for www.oceanlion.org -
   the domain's nameservers may be malfunctioning; DNS problem:
   SERVFAIL looking up AAAA for www.oceanlion.org - the domain's
   nameservers may be malfunctioning
Oops, something went wrong...
```

I hope to learn more about DNSSEC. In the meantime I’ve disabled it, it’ll take awhile to update.

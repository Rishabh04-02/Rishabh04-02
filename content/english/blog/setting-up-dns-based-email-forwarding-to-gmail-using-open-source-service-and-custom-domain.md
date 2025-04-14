---
title: "Setting Up DNS Based Email Forwarding to Gmail Using Open Source Service and Custom Domain"
meta_title: "Setting Up DNS Based Email Forwarding to Gmail Using Open Source Service and Custom Domain"
description: "Setting Up DNS Based Email Forwarding to Gmail Using Open Source Service and Custom Domain"
date: 2020-08-13T13:17:29+05:30
author: "Rishabh"
categories: ["DNS","email","technology","domain"]
tags: ["DNS","email","technology","domain"]
draft: false
---

## Prerequisite
1. A custom domain e.g. `https://google.com` .
2. A Gmail Account e.g. `MY_EMAIL@gmail.com` .
3. Account on `https://forwardemail.net` (free and open-source email forwarding service).

## DNS Management
1. Add MX Records and TXT Records in your domain manager (e.g. `name.com`, `namecheap.com`, `cloudflare.com`, etc.)

Note -
* You have to add these records to your current domain manager. Your current domain manager might be different from the one you purchased the domain.
* There should be NO other MX records set. If there were already MX records that existed, please delete them

2. After that choose the option how do you wish to forward the emails, by following the 4th point of the documentation.
3. Then add `v=spf1 a mx include:spf.forwardemail.net -all` as another TXT record.
4. Verify the MX and TXT Records using "Verify Records" tool on `https://forwardemail.net` .
5. Send a test email to confirm if it works.  Note that it might take some time for your DNS records to propagate.


Note -
* The above steps are just a brief summary of the DNS management. For the detailed process you can follow the documentation available at <a href="https://forwardemail.net/en/faq?domain=google.com#how-do-i-get-started-and-set-up-email-forwarding" target="_blank">How do I get started and set up email forwarding</a>.
* If you want to enable "How to Send Mail As" using gmail, you can follow the following documentation <a href="https://forwardemail.net/en/faq?domain=google.com#how-to-send-mail-as-using-gmail" target="_blank">How to Send Mail As using Gmail</a>.

---
title: "How Does ZeroNet Work?"
date: 2017-01-30T10:20:45+05:30
draft: false
project_url: "https://www.rishabhchaudhary.in/How_Does_ZeroNet_Work.md/"
Tags: ["Technology","Zeronet"]
Categories: ["Technology","Zeronet"]
keywords: ["Zeronet working","How does Zeronet work"]
---


* **The Basics of Asymmetric Cryptography**

When i create a new site we get two keys -

	Private Key 5JNiiGspzqt8sC8FM54FMr53U9XvLVh8Waz6YYDK69gG6hso9xu

    Public key 16YsjZK9nweXyy3vNQQPKT8tfjCNjEX9JM


a) Private key <code>5JNiiGspzqt8sC8FM54FMr53U9XvLVh8Waz6YYDK69gG6hso9xIu</code>

* Only **I have it**.
* It allows me to **sign new content** to the site.
* **No central registry**, it never leaves my computer. It don’t need to be published anywhere.
* **Impossible to modify** site without it.


b) Public key <code>16YsjZK9nweXyy3vNQQPKT8tfjCNjEX9JM</code>

* This is my **site’s address**.
* Using this anyone can **verify** that the content on the site is created by me (site owner).
* Every **downloaded file is verified** and hence makes it safe from malicious code’s insertion and modification.


**More info about Cryptography of ZeroNet**

1. ZeroNet uses the same elliptic curve based **Encryption as in your Bitcoin wallet**.
2. You can **accept payments directly** to your site address.
3. It is estimated that even using fastest supercomputer available, it would take around **1 billion years to “HACK” a private key**.

___________________________________________
---
title: "How to make your computer welcome you"
meta_title: "How to make your computer welcome you"
description: "How to make your computer welcome you"
date: 2016-01-06T10:11:43+05:30
image: "/images/image-placeholder.png"
author: "Rishabh"
categories: ["Technology","Windows"]
tags: ["Technology","Windows"]
draft: false
---

* Open **notepad** by searching it in the menu.

* **Copy** these lines as it is and **paste** them into your notepad.
```shell
Dim speaks, speech
speaks="Welcome back USERNAME "
Set speech=CreateObject("sapi.spvoice")
speech.Speak speaks
```

**Note** — You can replace **USERNAME** with your **Name**/**Username**.

* Save the file as **welcome.vbs** (on your desktop) or any other name with extension as **“.vbs”**.

* Go to **C** drive the view option on the menu bar and check the option **“Show hidden files”**.

* **Copy/Cut** the file from your desktop to the location -
```shell
Windows/Users/"USERNAME"/AppData/Roaming/Microsoft/Windows/Start Menu/Programs/Startup
```
**Note** — “USERNAME” — replace this with your username

* Paste the file in the Startup folder.

* Now login again and you’ll be greeted by your computer.

---
title: "GSoC - Completing the project"
meta_title: "GSoC - Completing the project"
description: "GSoC - Completing the project"
date: 2019-07-30T11:30:16+05:30
image: "/images/image-placeholder.png"
author: "Rishabh"
categories: ["GSoC","Libreswan","technology"]
tags: ["GSoC","Libreswan","technology"]
draft: false
---

![Google Summer of Code](/images/gsoc-logo.svg)


Previous post - [GSoC - Initial phase and getting selected](https://therishabh.in/gsoc_initial_phase_and_getting_selected/)

## First Evaluation
I was very excited at the beginning of the project, as it is a whole new experience, especially for a student. So, I started working on the project in May. The starting was challenging as I choose Django as the framework which the project is going to be built on, I did so because it was most suitable as per the requirements of the project. But I had never worked on it before. So, during the initial days, I spent a significant amount of time in learning Django. But this didn't slow the pace of the project. After working for around 10-15 days, all the configuration and tweaking were done, and the modules were written. So, after these days, the interface starts to work and perform the tasks it was supposed to do successfully. 

## Second Evaluation
After it starts to work and perform some of the functions we (when I refer "we," it means my project mentors and me) stepped past the 1st evaluations, and now were coding some complex functionalities. The work was going great when we realized that the support for Python 2.7 is going to end soon, so I had to restructure the whole interface and also upgrade the Django version. It took me a full day to restructure the entire interface, and at the end of the day, it was working again. At this point, I was creating modules which performed tasks ranging from generating OpenSSL certificates, certificates configurations, root certificates to performing email verification. All this was going great until I was stuck in a problem related to signing user certificates using the generated root certificates and configuration i.e., Generating CA-signed certificates. I was stuck with this problem for around 5 days, mainly due to the reasons that not much information was available regarding the same, my mentor was unavailable, no help from StackExchange either, and even after reading the OpenSSL documentation several times I could not figure out the solution. I almost quit trying at this time and wrote a mail to my mentor about the solutions I had tried and how they didn't work. After writing the mail, I was relaxed as my mentor has been working in this field for over 15 years and I was sure he'll find the solution to the problem. After that, I thought of giving it another shot and BOOM! I solved the problem this time, at this moment I was on cloud 9. I mailed the solution to my mentor and also pushed the code on GitHub. This was how the work in 2nd evaluation went.

## Final Evaluation
Now I entered the 3rd evaluation, and we implemented many things on the interface, fixed few issues, wrote documentation, performed some critical updates, added an administrators guide, automated some processes, and few other things. I went great until I got stuck again in the issue related to Certificate Revocation list and I can say that I resolved it in few days and the process very similar to the latter issue(Generating CA-signed certificates). This time too, I almost gave up. But kept going. And the interface was fully functional, and I had implemented all the things mentioned in my proposal and also some critical, required things. The interface was tested for a few days, and then I cleared my final evaluation.

## The Journey
The journey of GSoC 2018 has been great, there were many ups and downs on the way. But I got to learn a lot of things on the way (Thanks to the Mentors especially Tuomo; who explains things in a wonderful yet easy to understand way, The Libreswan Project, and Google of course). In the end, I can say it was worth the Effort, Time, Perseverance, during the process of creating a proposal and the part where the proposal is implemented into reality.

PS: The information regarding my project is available at [Libreswan wiki](https://libreswan.org/wiki/Libreswan_Managing_Interface).

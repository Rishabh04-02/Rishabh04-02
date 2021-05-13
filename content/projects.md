---
title: "Projects"
date: 2018-06-27T15:02:13+05:30
draft: false
project_url: "https://therishabh.in/projects/"
keywords: ["rishabh projects","rishabh chaudhary projects"]
---


## 1. [Libreswan Opportunistic IPsec using Let’s Encrypt](https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec/)
<img src="https://therishabh.in/gsoc-logo.svg" width="50%">

>	GSoC 2019, Bash(Shell Scripting), NSS database, Lets Encrypt, Certbot

Created shell scripts for establishing the Opportunistic Encryption connection using Libreswan IPsec. It also generates client/server configurations and updates and imports the certificates automatically along with handling files safely. Server/Client crashes handled. The project makes the process of using OE easier, automated and over 10 times faster than the manual procedure.

### Background  
Opportunistic IPsec is an attempt to encrypt the internet at large. The idea is to build VPN tunnels directly to all internet hosts irrespective of the communication used. An initial proof of concept was created that leverages LetsEncrypt certificates for use with IKE and IPsec. The goal of this project is to turn this proof of concept into production quality code that makes it trivial to enrol and deploy on any server and any client.

The project has the following objectives:

* Automate Client, Server configuration and the enrollment and updating of LetsEncrypt certificates for use with libreswan.
* Implement a DNS/DNSSEC based method for advertising Opportunistic IPsec support using LetsEncrypt for servers.
* Design a non-DNS based method for publishing support of LetsEncrypt based Opportunistic IPsec for servers.
* Enhance libreswan to allow a secure fallback to the existing NULL Authentication method.
* Ensure the working of two behind the same NAT. Along with ensuring the working of two clients behind NAT, with one not using IPsec.
* Support the recovery from server OR client reboot/crashes. Along with ensuring no lockouts happen.

___________________________________________

## 2. [Libreswan managing interface](https://github.com/Rishabh04-02/Libreswan-managing-interface)
<img src="https://therishabh.in/gsoc-logo.svg" width="50%">

>	GSoC 2018, Django 2.0, Python 3.5, MySQL, HTML-CSS  

Developed Application for generating & signing CA root certificates & user certificates (VPN connection profiles) along with generating custom configurations for user certificates. Automatic creating and updating of certificate revocation list implemented. The project increased the efficiency of performing all the above tasks by over 7 times as compared to the existing manual procedure.

### Background  
There   are   shell   scripts   for   creating   X.509   certificates,   revoking   certificates   and  signing   CRLs   and   scripts   for   the   creation   of   Profile   certificate   files   for   certain  devices   such   as   Linux,   Apple   OS   X,   Windows,   iOS,   etc.,   these   require   careful  specification   of   various   certificate   attributes   so   that   these   certificates   work   on   a  variety   of   devices:   Android,   Windows,   iOS/OSX,   Linux,   etc.   The   goal   of   this   project  is to gather all that knowledge into a simple interface.

The interface supports the following:

* Generating   the   proper   ipsec.conf   configuration   based   on   web   admin  interface including DNS/split-DNS configurations.
* Allow Administrator to invite new users using email id.
* A   new   user   after   account   validation   can   download   the   generated  certificate/profile (over TLS) for different platforms.
* The   generated   certificates/profiles   can   only   be   downloaded   once,   through  the portal.
* Admin   can   list,   revoke/disable   (temporary   revocation)   user  certificates/profiles.
* Generate PKCS#12​ certificates for users.
* Generate   iOS/OSX   ​ .mobileconfig   profiles   for   automatic   installation   on  iOS/OSX.
* Ipsilon user authentication to web application.
* Configure munin-node to work with libreswan plugin.

___________________________________________

## 3. [Linux based secure systems manager](https://github.com/Colviz/Vince/)
>	Python, Sockets, GPG (GNU Privacy Guard), Linux, Broadcasting

Allowing the system administrators to perform different tasks parallelly on 100’s of the client systems. It has error detection and correction functionality, along with providing real-time support for clients. The payload sending is secured with PGP key encryption. This project increases the efficiency of performing the above tasks by over 30 times as compared to the manual procedure.

## Background
This project is Developed and submitted (as Major Project II) in partial fulfillment of the requirements for the award of the degree of Bachelor of Technology and is the continuation of project: Agent using client server Interaction.

This project named Linux based secure systems manager, is an open source software. It allows the system administrator to perform various tasks on the client systems connected on a network with just firing a command eg. installation of softwares, upgrading system, shutting down the systems, which then performs/executes the desired tasks on all the systems. Also, it allows various users on a network/subnet to chat in a dedicated chat room. This software can easily adapt to large network of computers and works efficiently for small networks.

This software can be used in any computers connected to a single network with Linux as the operating system like a computer laboratory. The only constraint is that they all must run Linux as their operating system with python and Thefuck (package) installed along with few modules of python eg. python3-tkinter. The project uses the package Thefuck for error correction. The client scripts can be installed using !bangs in Linux.

Thefuck for error handling and error correction tries to match a rule for the previous command, creates a new command using the matched rule and runs the corrected command. Moreover, we can also create our own rule for the package and in that way it’ll become more effective and efficient according to our needs. Also the error correction package we are using is open source and hence is under rapid development phase and also its available for all available major operating systems.

___________________________________________

## 4. [Agent using client server Interaction](https://github.com/Colviz/Vince/tree/abb8c829f1b7b92a3c58c94f7bb2f61730f4ae34)
>	Python, Sockets, Linux, Broadcasting

## Background
This project is Developed and submitted (as Major Project I) in partial fulfillment of the requirements for the award of the degree of Bachelor of Technology.

This project named “Agent using client server Interaction”, is an open source project. It will allow the system administrator to perform certain tasks on the client systems connected on a network with just firing a command, which will then perform the set of desired tasks on all the systems. This set of desired tasks can be anything ranging from installing a particular software on systems to downloading and executing some available script. This software can easily adapt to large network of computers and works efficiently for small networks.

This software can be used in any computers connected to a single network like a computer lab. The only constraint is that they all must run Linux based OS with python and Thefuck (package) installed. The project uses the package Thefuck for error handling and error correction. The client scripts can be installed using !bangs in Linux.

___________________________________________

## 5. [Elective Manager](https://github.com/Rishabh04-02/Elective-manager)
>	PHP, MySQL, Javascript, HTML-CSS, Material Design						  

Built an application for the online allotment of various UG/PG electives, which are allotted based on CGPA, elective priority & available seats. The software has an auto backup mechanism and is using SQL procedures for performing various tasks. The project has proved to be over 15 times faster than the existing system (manual).

### Background
This project named Elective Manager, is an open source project. It will be used to allot the Elective subjects to undergraduate as well as post-graduate students. These elective subjects are published by the departments and are allotted to students based
on their priority of published subjects and CGPA. The system can adapt to a range of events from small scale to large scale.

Previously, the allotment of the elective subjects was done manually which was a very inconvenient method for the students as well as for the teachers. The allotment process was very chaotic and time consuming.
The Prime objective of this project is to automate the process of allotment thus allotting the elective subjects without chaos and in a more convenient manner to the people involved.

___________________________________________

## 6. [Training and placement portal NITH](https://github.com/Rishabh04-02/Training-and-placement-portal-NITH)
>	Django, Python, Mysql, Javascript, HTML-CSS

Developed Official website - Office of Training and Placement NIT Hamirpur. It eases the process of finding the relevant info regarding the Placement cell and helps with the process when visiting the Institute for placements. The project has turned out to be over 10 times faster than the existing procedure.

### Background
This project is the website of Office of Training and Placements NIT Hamirpur (H.P.) India - 177005.
This portal is made to reduce the effort by the visitors (students/companies/organizations) in finding the relevant information regarding the Placement cell NIT Hamirpur and also for ease of access when visiting the institute for placements.
This portal will also allow the Office to share the content/latest information with the students/organizations easily and fast.
This portal has all the relevant information on it be it about the functionaries, internships, placements, previous records OR information on how to reach the institute. Also the latest placement news and placement briefs keeps flashing on the screen along with the list of present recruiters.

___________________________________________

## 7. [Paradox - Team .EXE](https://play.google.com/store/apps/developer?id=Team+.EXE)
>	PHP, MySQL, Javascript, API, HTML-CSS

An online game, with answers based on an image/set of images. Hints are provided periodically. Website and App work on APIs. The App has 50K+ downloads on Google play store and receives 5K+ monthly registrations.

## Background
Paradox is a globally acclaimed event that is organized before as well as during NIMBUS by Team .EXE , the departmental team of Computer Science and Engineering of NIT Hamirpur.
It is an online level based game where the participant looks for a "word" that is signified by an image/set of images. Hints are provided periodically to help with the process of thinking in the right direction. It is open for participation from the students of the college as well as globally.
One can participate in the event through the paradox website or its app. The website and the app works on the API.
I've developed Paradox for 3 consecutive years - 2016, 2017, 2018.

___________________________________________

## 8. [Life Cycle](https://github.com/Rishabh04-02/Life-cycle)
>	C++, OpenGL, Graphics.h

### Background
This project aims at describing the life cycle of a common person with the help of a character named SUDO. In this project Sudo covers all the basic life experiences and changes which we humans encounter during our life cycle. If this project needs to
be categorized then the category under which it falls will be - A short film, but that in graphics mode and made with OpenGL.
OpenGL language is used in making of this project and it uses various advanced tools of Computer graphics.

OpenGL - It’s the most powerful language available for Computer Graphics and to prove this statement we can see that all the operating systems runs on OpenGL to display their Graphics output and its by default installed in every OS so as to display Its GUI (graphical user interface).

___________________________________________

## 9. [Uploadbin](https://github.com/Rishabh04-02/uploadbin)
>	PHP, MySQL, Javascript, HTML-CSS

The portal allows the users to upload and share files online. When a file is uploaded, a sharing link is generated which will allow the downloading of the file. Also, the admin can review and delete the files whenever needed. It can be installed on intranet and can make the file sharing 5 times faster.

### Background
It lets the user upload and share files online. When a file is created a link is generated which will download the file on opening. One can share the link to the people one want to share the file. Also the admin can review and delete the files whenever needed. This was developed to submit assignments online as this will be running on a local server so that makes uploading and sharing files really easy and fast.

___________________________________________

## 10. [Article Management System](https://github.com/Rishabh04-02/article-management-system)
>	PHP, MySQL, Javascript, HTML-CSS

Web Application allowing the Professors to give assignments to students. The students can see the assignment along with the submission deadline and can submit the solutions accordingly. The teacher then evaluates the assignments. It increases the assignment submission and evaluation efficiency by over 5 times.

### Background
It is a management system where the teacher can give assignments/programming questions to students of a respective branch/group. The students can see the assignment on their interface and can submit the solutions respectively for each question/assignment as per the requirements set by the teachers.

The interface has the following features:

* It has a different interface for student and teacher login/registration.
* Teacher can post questions lab wise and question wise.
* Teacher can view submissions of all the students lab wise.
* Teacher can view all the submissions of students of every lab sorted roll. no. wise.
* Teacher can check for plagiarism and then report it to students.
* Student can view questions lab wise.
* Students can submit their programs lab wise.
* Students can view all their submitted programs lab wise.
* Students can change any of their program at any time of any lab.

___________________________________________

<!-- Prepare a container for your calendar. -->
<script src="https://cdn.rawgit.com/IonicaBizau/github-calendar/gh-pages/dist/github-calendar.min.js"></script>
<!-- Optionally, include the theme (if you don't want to struggle to write the CSS) -->
<link rel="stylesheet" href="https://cdn.rawgit.com/IonicaBizau/github-calendar/gh-pages/dist/github-calendar.css"/>
<!-- Prepare a container for your calendar. -->
<div class="calendar" style="width:auto; overflow-x:scroll">
    <!-- Loading stuff -->
    Loading the data just for you.
</div>
<script>
    new GitHubCalendar(".calendar", "Rishabh04-02");
</script>

---
title: "Few things about WannaCry ransomware"
meta_title: "Few things about WannaCry ransomware"
description: "Few things about WannaCry ransomware"
date: 2017-05-20T12:24:09+05:30
author: "Rishabh"
categories: ["Technology","ransomware"]
tags: ["Technology","ransomware"]
draft: false
---

A global cyber attack has been underway since Friday 12 May 2017, affecting more than 200,000 organizations and 230,000 computers in over 150 countries. It has been described as unprecedented in scale.

Well It’s ```source code is not yet available```, but below is some information that can be useful in understanding its structure and behavior.

* **Virus Name**: WannaCrypt, WannaCry, WanaCrypt0r, WCrypt, WCRY
* **Vector**: All Windows versions before Windows 10 are vulnerable if not patched for MS-17–010. The malware is using the EternalBlue (MS17–010) exploit to distribute itself. This is a SMB vulnerability with remote code execution options.
* **Ransom**: between $300 to $600. There is code to ‘rm’ (delete) files in the virus. Seems to reset if the virus crashes.
* **Backdooring**: The worm loops through every RDP session on a system to run the ransomware as that user. It also installs the DOUBLEPULSAR backdoor. It corrupts shadow volumes to make recovery harder. Ransomware is writing itself into a random character folder in the ProgramData folder with the filename tasksche.exe or in the C:\Windows\ folder with the filename mssecsvc.exe and tasksche.exe.
* **Kill switch**: If the website ``www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com`` is up the virus exits instead of infecting the host. This domain has been sinkholed, stopping the spread of the worm. Will not work if proxied.
* **File size** of the ransomware is 3.4MB (3514368 bytes).
* The ransomware **grants full access** to all files by using the command:
     ``Icacls . /grant Everyone:F /T /C /Q``
* Using a batch script for operations:
     ``176641494574290.bat``
* **Content of batch file** (fefe6b30d0819f1a1775e14730a10e0e)

<pre>
echo off
echo SET ow = WScript.CreateObject(“WScript.Shell”)> m.vbs
echo SET om = ow.CreateShortcut(“C:\WanaDecryptor.exe.lnk”)>> m.vbs
echo om.TargetPath = “C:\WanaDecryptor.exe”>> m.vbs
echo om.Save>> m.vbs
cscript.exe //nologo m.vbs
del m.vbs
del /a %0
</pre>


**Content of M.vbs**


    SET ow = WScript.CreateObject(“WScript.Shell”)
    SET om = ow.CreateShortcut(“C:\
    WanaDecryptor
    .exe.lnk”)
    om.TargetPath = “C:\
    WanaDecryptor
    om.Save


**Cryptography details**

* Each infection generates a new RSA-2048 keypair.
* The public key is exported as blob and saved to ``00000000.pky``
* The private key is encrypted with the ransomware public key and saved as ``00000000.eky``
* Each file is encrypted using AES-128-CBC, with a unique AES key per file.
* Each AES key is generated CryptGenRandom.
* The AES key is encrypted using the infection specific RSA keypair.
* The RSA public key used to encrypt the infection specific RSA private key is embedded inside the DLL and owned by the ransomware authors.


**Encrypted file format**

    typedef struct _wc_file_t {
     char sig[WC_SIG_LEN] // 64 bit signature WANACRY!
     uint32_t keylen; // length of encrypted key
     uint8_t key[WC_ENCKEY_LEN]; // AES key encrypted with RSA
     uint32_t unknown; // usually 3 or 4, unknown
     uint64_t datalen; // length of file before encryption, obtained from GetFileSizeEx
     uint8_t *data; // Ciphertext Encrypted data using AES-128 in CBC mode
     } wc_file_t;



**Command & Control centers**
<pre>
gx7ekbenv2riucmf.onion
57g7spgrzlojinas.onion
xxlvbrloxvriy2c5.onion
76jdd2ir2embyv47.onion
cwwnhwhlz52maqm7.onion
</pre>

**Bitcoin Wallets**
<pre>
115p7UMMngoj1pMvkpHijcRdfJNXj6LrLn
13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94
12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw
</pre>

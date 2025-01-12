---
title: "Passbolt"
description: "Provides installation instructions for the Passbolt application in TrueNAS."
weight: 
aliases:
tags:
- apps
- password manager
keywords:
- nas data storage
- software storage solutions
- flash storage
- password managment
---

The TrueNAS Passbolt app installs the Passbolt password manager. Passbolt is a free app that allows you to store your passwords localy and let's you access them anytime as long as you have access to your network.<!-- is a [description of the application] -->

{{< include file="/static/includes/apps/CommunityApp.md" >}}

## Before You Begin

It is importent to note: Unless you are planning to use the mobile app of Passbolt, HTTPS is not strictly required but highly recommended by passbolt. To enable HTTPS for passbolt, you will be asked to create or import a new SSL certificate.

Go to **Credentials > Certificates** and select in the section marked **Certificates** click **ADD**

fill out all the nessisary information, (This article will assume you chose to make an internal Certificate) if you reach the feild labled **Signing Certificate Authority** and clicking the drop down shows nothing, you will need to exit and create a Certificate Authority, which is largly the same process. Click **ADD** in the **Certificate Authority** section to do so.

in part 3 of creating the Certificate, you will be asked for a **Common Name**, and a **Subject Alternative Name** these, for a self signed Certificate, should be filled with either "localhost" or your server's IP adress or Domain. **domain.example*

With that out of the way, we can now start installing Passbolt!

## Installing Passbolt

Go to **Apps** in the upper right click ***Discover Apps** then search for Passbolt, then click install.

fill in the required feilds. for **App URL** type "HTTPS://&lt;your.Domain&gt;" or if you don't have a domain, "HTTPS://&lt;your.local.IP:Port&gt;" You can find the correct port just below in the **Network Configuation** section. under **WebUI Port**

Passbolt recommends you to **ADD** a new feild to **Additional Environment Variables**. for **name** type:"PASSBOLT_SSL_FORCE", for **value** type:"true".

Now, under **Network Configuation** click **Certificate** and select a Certificate (if you are not enabling HTTPS change the **APP URL** to start with "HTTP" rather than "HTTPS" and skip this step.)

fill out the rest of the form and then click **INSTALL** down at the bottom.

Congrates! Passbolt is now installed, but if you were to select Passbolt and click **Web UI** you would see a promt for your email. and once filled it will trow you an error saying you are not registered. Let's fix that

## Registering Admin

go back to the **Apps** section on TrueNAS. from there select Passbolt and on the left you should see a section called **Workloads**. In this section find **Passbolt** and click the terminal looking thing. (when hovering over it, it will say "Shell") you should see a black box with a "$" on the top right, and a cursor blinking right beside it.

Here you need to type the command:

"/usr/share/php/passbolt/bin/cake passbolt register_user -r admin -u &lt;Your@email.com&gt; -f &lt;first_name&gt; -l &lt;last_name&gt;"

make sure to fill in the &lt;&gt; with your information.

you should see passbolt say that it will send you a link of what to do next via email. sadly this is probably a lie. luckilly it also gives you the URL, so take it and type it into your browser. You should be greeted by a screen that says something along the lines of "Create your passcode".

follow it's instructions untill you reach the password page. you are almost done!!!

## Email Server

Go to **administration** and **Email server** you will need to fill this out.

If you don't know how follow this guide from Passbolt: https://www.passbolt.com/docs/admin/emails/email-server/

be warned, the Passbolt documentation does not work well with TrueNAS, once you reach **Configure SMTP server using custom/self-signed certificate** it will no longer be helpfull to you.

once you have your email server set up, make sure you save and then test.

and congradulations! unless you used a self-signed certificate for HTTPS and want mobile functionality, you are done!!! you can now use passbolt on any computer you own, provided it has the passbolt extension installed on your browser.

## Mobile Functionality

assuming you didn't use a self-signed certificate for HTTPS it should be working, follow the steps provided by Passbolt.

if you used a self-signed certificate, then you will need to download and manually trust the root certificate for each mobile device you plan to add.

follow this guide from Passbolt:

https://www.passbolt.com/docs/hosting/faq/how-to-import-ssl-certificate-on-mobile-application/

Make sure you download the root certificate .CRT file, if you crated a "Certificate Authorty" earler, that's what you need.

Once that is all done, download the mobile app for Passbolt and scan the QR codes in the **Mobile** section of the passbolt WebUI.

Now it is over, everything is set up, and all you have to do is input all of your passwords. enjoy!

<!-- Comment out the following line if your suggested changes to this Community app documentation provide a complete installation tutorial. Leave exposed if you are proposing a partial expansion of the content, but further work is needed. -->
<!--{{< include file="/static/includes/apps/CommunityPleaseExpand.md" >}}

<!-- Uncomment the following line if you suspect this Community app documentation is out of date, inaccurate, or needs further improvement -->
{{< include file="/static/includes/apps/CommunityPleaseImprove.md" >}}-->

<!--{{< include file="/static/includes/ProposeArticleChange.md" >}}

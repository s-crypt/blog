---
layout: post
title: Stuff I Wish I Knew Faster
tags:
  - information
---

##### I spent too long trying to find these answers, so here is what I discovered.
##### They will be updated with time as I remember them.
---

  
#### Does watchos 7+ support encrypted DNS (DoH)?
No. only iOS, tvOS, and macOS
<br/><br/>

####  Does wireless charging hurt your phone?
Undecided but leaning toward 'worse than cable charging'. Weigh the benefit of a battery degrading faster due to heat with the port degrading faster. 
<br/><br/>

#### Is fast charging bad?
 No. Lithium ion batteries are fine with full speed charging until 80%, where it slows to preserve battery lifespan. The main limit is heat, as heat is the most dangerous thing for your battery. EDIT: A nice video on the subject by MKBHD. [LINK](https://www.youtube.com/watch?v=UpqaQR4ikig)
<br/><br/>

#### Is the Dream Machine Pro (UDM-Pro) a DHCP Server?
Yes. All you need is a modem. There is an option to have the UDM-Pro be the DHCP server or forward DHCP requests to a different IP. There are options to customize the UDM-Pro's DHCP server and the ability to assign static IPs through the client devices page.  
The connection is: ISP Cable -> Modem -> UDM Pro -> Switch -> Devices/APs
<br/><br/>

#### Does the Unifi Controller support DNS over HTTPS (DoH)?
Not yet, but you can set up the NextDNS CLI or [cloudflared](https://developers.cloudflare.com/1.1.1.1/dns-over-https/cloudflared-proxy/) with whatever server you want by SSH-ing into the server (not the network controller, but set up ssh in the controller settings).  
Instructions for the NextDNS CLI [here.](https://github.com/nextdns/nextdns/wiki/UnifiOS)
<br/><br/>

#### Why does my Ethereum transaction run out of gas for ENS Domains?
Ethereum transactions between wallets need 21000 gas, while smart contracts need a lot more, in the range of 300,000. Let your wallet choose the correct gas limit, and change the gwei to the desired amount.
Be careful, the transaction fee is still consumed even if the transaction fails.
<br/><br/>

#### Why can't I register my .xyz domain with ENS?
I got the error `Could not find a DNSKEY record to validate any RRSIG on TXT records for _ens.domain.xyz` when trying to register a gTLD on the Ethereum Name Service. Make sure that you are using Algorithm 8 and **NOT** Algorithm 13 for DNSSEC. Only a few DNS providers allow you to do this, and most default to Algorithm 13, so make sure this is the case. 
Currently ENS needs Algorithm 8 (which is a RSA key) rather than Algorithm 13 (which is an ECDSA key) due to the cryptographic nature of crypto wallets. 
ECDSA is objectively better, but apparently support for it on ENS is a work in progress for now.

EDIT: This now works, but costs a prohibitively amount of gas so unless gwei goes way down, purchasing an ENS domain is cheaper.
<br/><br/>

#### What happens if I have over the FDIC Desposit Insurance Limit and the bank fails?
Not totally sure, as I am pretty sure the case hasn't arisen yet. Most likely all of your assets will get transferred to the bank that is taking over the failing one.
<br/><br/>

#### How do I stream audio from iOS to Windows?
You will need bluetooth enabled (buy a dongle if you are using a desktop without BT). In short, windows 10 v2004+ have the capability to stream audio through bluetooth (called A2DP Sink), but no implementation. The explanation below describes a tool that implements the bluetooth audio streaming. (all the screen mirroring apps and the like are sketchy as heck)
[See this excellent answer on superuser](https://superuser.com/questions/1199132/is-there-any-way-to-make-windows-10-act-as-a-a2dp-sink)
[Tool Repo](https://github.com/ysc3839/AudioPlaybackConnector)
<br/><br/>

#### Can you use a SD card AND the cellular / wireless connection with a ResMed AirSense 11?
Yes, according to [this forum thread](http://www.apneaboard.com/forums/Thread-ResMed-Airsense11-software), and this response from ResMed Customer Support:
"You may use an SD card to locally store your data the machine records and bring in the SD card for your provider for anything from compliance to report print-outs. Both [cellular and SD card] can be used simultaneously and your machine will always have 365 days of data on it's local storage."
To Note: When inserted, the SD card will be backfilled with data that was onboard although at a lower frequency. When an SD card is used, the device records data at more frequent intervals than without one.
<br/><br/>

#### How do you export all contacts on iPhone (with contact pictures)
All the apps for this are garbage, probably vaccum data, and don't do what they advertise and no other methods I have found work. To actually export contacts (iOS 16):
1. Open the Contacts app
2. Navigate back at the top left to "Lists"
3. Press and hold on the list of your choosing, like "All iCloud"
4. Press Export
5. Export to the place/app of your choosing

The contacts will be bundled as one vcf file with all of your contacts information inside, including images.
<br/><br/>

#### Why is my brand new image of Homebridge not connecting to wifi?
This seems to be an error with the most recent debian image bundle with bullseye and WPA3. Connect manually to the device with cables and use `hb-config` to change the wireless network's properties to use WPA2 and restart the device.
<br/><br/>


#### How do I reset an HP Pagewide Pro (400 and 500 series) that is locked with an admin password?
I was able to reset the printer after searching through forums. Here is what worked for me.
1. Turn the printer off and disconnect everything but the power cable
2. Press and hold the power button for about 20 seconds until the buttons on the left of the touch screen light up. Let go
3. Press and hold the ? button for 30 seconds. Let go
4. Press the home button (may have to hold for a few seconds)
5. A boot menu will pop up. Use the PREV and NEXT buttons to navigate to FULL RESET and press OK
6. Let the printer boot
7. Set up as IT Pro and follow instructions. Do not connect to internet
8. Once the printer is initalized, go and reset the printer from the settings screen because the embedded web server is still locked

#### How do I set up a Python Virtual Environment for a Jupyter notebook using VS Code?
You can create a new virtual environment for your Jupyter notebook, but it isn't automatic. 
1. Open the terminal in VS Code and navigate to the directory your notebook is in*. Then type `python -m venv .venv` 
	1. This will create the virtual environment in a folder named `.venv`
2. At the top right, click on the python kernel you are using for your notebook (It will say `Python 3.12` and whatever version of python you are using)
	1. VS Code might suggest to switch to the virtual environment in a popup. You can just click yes to switch to it.
3. Click on venv(`Python 3.12`) with whatever version of python you are using.
4. Done! VS Code will prompt you to install the `ipykernel` package when you run code for the first time because it is needed for the notebook's code execution.

\*You can configure what folder the terminal opens in by default with `terminal.integrated.cwd`. I set it to `${fileDirname}` because I always want it to open in the folder of the file I am working on.
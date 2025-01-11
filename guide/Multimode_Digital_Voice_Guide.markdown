---
title: Multimode Digital Voice Guide
---


<body style="background-color:powderblue;">
<style>
body {
      margin: 0 auto;
      max-width: 100em;
      padding-left: 100px;
      padding-right: 100px;
      padding-top: 50px;
      padding-bottom: 50px;
      hyphens: auto;
      overflow-wrap: break-word;
      text-rendering: optimizeLegibility;
      font-kerning: normal;
    }
</style>


## <span style="color: blue">Digital Modes Summary</span>

With the significant upgrade of a Raspberry Pi[^1] (RPi) running IcomGateway,[^11] and the connection of KR4CHS to a transcoding[^3] reflector, KR4CHS is transformed into a Multimode Digital Voice system.

The following Digital modes are currently supported.

1. D-STAR[^4] - Direct to Repeater and via hotspot
2. DMR[^5] - via hotspot
3. YSF[^6] via hotspot
4. M17[^7] via [**mvoice**](https://github.com/n7tae/mvoice) on Linux or hotspot

Operators of these devices can have QSOs, not limited by mode type. 

## <span style="color: blue">KR4CHS Standard Reflector Linking</span>

KR4CHS is linked to Reflector[^8] XRF517 Module A as the repeater's standard reflector and module.

## <span style="color: blue">Modules Enabled</span>

1. \(A\) Transcoding for D-STAR, DMR, YSF, and M17
2. \(B\) DMR and YSF
3. \(C\) M17
4. \(D\) D-STAR
5. \(E\) Development

## <span style="color: blue">Transcoding Modes Access - XRF517A\*</span>

| Mode | Access |
| :---| :--- | :--- |
|D-STAR  | KR4CHS, Awendaw, SC 145.210 -0.600 MHz |  
|D-STAR    | XRF517A |  
|DMR  |   QuadNet 517 | 
|DMR  |   XLX_517 Module A (4001) | 
|DMR  |   TGIF 517 ||
|YSF  |   YSF51700 - US-URF517 - RadioSC |
|YSF  |   YCS310 DG-ID 81 |
|YSF  |   FCS31081 |
|M17  |   URF517A |

\*For more detailed help see the next section.

## <span style="color: blue">Digital radio connection with Module A</span>

Module A of the reflector is the module which will allow QSOs between D-STAR, DMR, YSF, and M17 operators.

### D-STAR direct to Repeater

Set your D-STAR radio as follows (uses KF5CJG as an example)

UR: CQCQCQ             Use Repeater   (this doesn't say Reflector but it's Ok)  
R1: KR4CHS C           Charleston     
R2: KR4CHS G           Charleston G  
My: KF5CJG /5100 

R2 should always be set to "G," Gateway,[^2]  to avoid QSO confusion and doubling with Hotspot operators and non-KR4CHS repeater operators.  Though you will hear those other operators, they will only hear you if you are on the Gateway.

### D-STAR via a hotspot[^12]

Using KF5CJG's hotspot as an example first link to XRF517A:

UR: XRF517AL              
R1: KF5CJG B      
R2: KF5CJG G  
My: KF5CJG /5100 

After setting your radio as above, PTT.  Your hotspot should report that you are linked to XRF517A.  Linking to DCS517A also works.

Next, change UR from XRF517AL to "Use Reflector."  After selecting "Use Reflector," the "CS" screen on your D-STAR radio will display the following:

UR: CQCQCQ   \     \     \    Use Repeater              
R1: \<YourCallSign\> B      
R2: \<YourCallSign\> G  
My: \<YourCallSign\> /\<YourText\>  


### DMR via XLX Master

In your Pi-Star set the DMR Master to: “DMR Gateway” then ensure XLX is enabled. For WPSD hotspots make sure XLX Master Enable is on.

Select XLX_517 from the drop-down box, then select module A. If the above selection does not show in the drop-down menu, run the Update on Pi-Star found in the admin menu.

For your radio, add a channel with Talkgroup[^9] 6 (Group Call) into a zone[^13] of your choosing. A zone named RadioSC is a good choice.

Once XLX_517 Module A is set in your hotspot, select the Talkgroup 6 channel on your radio and you should be set for your first QSO on the Reflector. 

### DMR via QuadNet Talkgroup (TG) 517

In the latest version of WPSD, the DMR master is user-selectable.  Prior to this WPSD set the the DMR master to Brandmeister so that all other Networks required a TG prefix.  Now, since WPSD allows the selection of the DMR master, the user can choose the DMR Network that does not require a TG prefix.  
![QuadNet as Primary Network](C:\Users\nick\SynologyDrive\Atom/radiosc-info\images\Primary-DMR-Network.png)

If using WPSD an "8" prefix is required for the TG create a Talkgroup so on your DMR radio create an 8000517 TG. A total of seven digits is required so fill between "8" and "517" with three zeros.  Create a channel for your new TG and add the channel to a zone.

Go to WPSD Configuration, scroll down the "DMR+/FreeDMR/HBlink/Custom Network Settings" and select "HB_US_Quadnet_1_GA" as this is the geographically closet server.

If you want TG 517 to be static (reccommended) then enter the following in Options:

"TS2=517;TIMER=10;VOICE=0,DIAL=0"  (no quotes)

In order to add more static TGs separate them with commas (e.g. TS2=517,320,321).

In order to view activity go to the menu of all [**QuadNet Rysen servers**](https://quadnet.ddns.net/) and click on the dashboard picture of the Atlanta server dashboard which will then display the Atlanta Rysen server.

### DMR via TGIF TG 517

Enable TGIF DMR for WPSD or Pi-Star.  A user account and security key from TGIF is required.  Depending upon the configuration in your hotspot software, a TG prefix may be required.


### Yaesu System Fusion (YSF)

In your YSF PI-star set the YSF startup host to:

“YSF51700 - US-URF517 - RadioSC”

For your radio simply set the VFO to the frequency of the Pi-Star or WPSD hotspot and the mode to DN. Or create a memory channel with the hotspot frequency and DN mode.

### QuadNet YSF access to XLX517A

There are two QuadNet connections to the XLX517 transcoding module A:

* YCS310 DG-ID 81 [YC310 Dashboard](https://ycs.openquad.net/)

* FCS31081 [FCS Dashboard](https://dmr.openquad.net/#)

### M17

Install mvoice on a Ubuntu 24.04 or Debian 12 computer or connect via a hotspot and a Connect Systems M17 radio.

Operators who desire to use M17, which we encourage, should contact the RadioSC team for assistance.

## <span style="color: blue">Module Connection Table</span>

| Module | Name       | D-STAR DExtra  | DMR TG 6      | YSF    | YSF DG-ID | M17      |
| :---| :--- | :---                 | :---:        | :---   | :---       | :---    |
|A    | Transcoding | XRF517AL      | 64001     | #51700    | 10      | URF517A |
|B    | DMR, YSF | -                 | 64002    | #51700    | 11      | -       |
|C    | M17         | -              | -           | -         | -       | URF517C |
|D    | D-STAR      | XRF517DL       | -           | -         | -       | -       |

## <span style="color: blue">KR4CHS D-STAR repeater operating modes</span>

1. Repeater is not connected to a Reflector - supports D-STAR local operators
2. Repeater is connected to a Reflector - supports D-STAR local users and Internet-based operators

### Mode 1
All operators within RF range of the repeater can make local calls on the repeater and connect to Reflectors for making calls. In other words, all normal D-STAR capability is available to the operator within RF range of the repeater.

### Mode 2
To Mode 1 add all hotspot (and dongle, etc.) operators (those local and worldwide). Hotspot operators can connect to the Reflector that the Repeater is linked to and have QSO's with all Reflector-connected operators and local operators (Note: The best operating practice for Mode 1 operators is to always have R2 set to Gateway. Otherwise if a QSO is in progress on the Reflector the local operator on KR4CHS will hear the reflector via the repeater but Gateway operaters will not hear the local operator which among other things could cause doubling and could cause Reflector users to "step on" a local QSO.)

## <span style="color: blue">Reflector linking options</span>

KR4CHS is capable of linking to virtually all reflector types except M17 reflectors (mrefd) as M17 only reflectors (mref) are designed for M17 only.  However, universal reflectors, like URF517, includes M17 capability and we have reserved Module C for M17 to M17 QSOs.

The first four reflectors shown below are DPlus reflectors.  These reflectors are for D-STAR QSOs only.  These are shown for completeness but are not preferred as the new capabilities of KR4CHS, namely its multimode capability are not possible with DPLus reflectors.

1. REF001C - The D-STAR Mega Reflector - Lots of activity worldwide on D-STAR only - no transcoding between modes.
2. REF030C - Wide Area linked repeaters - similar to REF001C in activity. D-STAR only.
3. REF054C - Carolinas Repeaters, based out of Charlotte. D-STAR only.
4. XRF757A - QuadNet Transcoding Reflector for D-STAR, DMR, YSF, and M17.
5. Any other Reflector using the REF or XRF protocol for ad-hoc or scheduled purposes.  Connection via the XLX protocol is not supported.

## <span style="color: blue">Reflector Linking / Unlinking Protocol</span>

Note: Linking and Unlinking the D-STAR Awendaw Repeater can only be accomplished with a D-STAR radio.

If an operator wants to link to a Reflector other than XRF517A, first listen to determine if the Repeater is currently in use.  If not in use, announce your intention to link to your desired Reflector.  Then unlink the Repeater.  After unlinking, link to your desired reflector.  Complete your QSO, then unlink and link back to XRF517A, returning the repeater to its normal state.

## <span style="color: blue">Selected D-STAR Nets</span>

### North Carolina & Friends of D-STAR Net

Tuesday  9:00pm on REF054C.

### Coastal Carolina D-STAR Net

Saturday at 7:30pm on REF054C.

### Raspberry Pi Net

Monday at 11:00pm on REF038C.

### D-STAR Tech Net

Tuesday @ 11:00pm on REF012A.

More [**Papa System info**](https://papasys.com/events/dstar-tech-net/)

## <span style="color: blue">Multimode Digital Voice Nets</span>

### Digital Dog Net

Every Monday starting at 5pm EDT on RadioSC.

Logging on [**Ham.live**](https://ham.live)

### RadioSC Multimode Net

First Monday of each month at 7pm EDT on RadioSC wtih early check-in beginning at 6:45pm.

Logging on [**Ham.live**](https://ham.live)

### QuadNet Multimode Digital Voice Net

Saturday @ 6:00pm EST on Reflector XRF757A.

D-STAR XRF757A.

QuadNet Talkgroup 320.

TGIF Talkgroup 320.

YSF31001.

M17 URF587A.

### Other Nets on QuadNet

Visit [**QuadNet**](https://openquad.net/) to the QuadNet Net schedule.

## <span style="color: blue">Building your own Raspberry Pi-based Hotspot</span>

A Raspberry Pi (RPi) is a single board computer that when paired with a MMDVM (Multimode Digital Voice Modem) and loaded with free open source software contained on a Micro SD card and connected to the Internet becomes your very own little repeater that gives the operator access to multiple digital modes (D-STAR, DMR, Yaesu System Fusion, M17, and others) and their associated Reflectors, Talkgroups, and Rooms[^10].

There are at least two operating system options that will run a hotspot, [**Pi-Star**](https://www.pistar.uk/) and [**WPSD**](https://w0chp.radio/).  As mentioned one of these OS images must be loaded onto a Micro SD card that will be inserted into the Raspberry Pi.

### Purchase all necessary hardware:

Several different Raspberry Pi Board models will run a Hotspot.  The least expensive recommended Pi board is the Pi Zero 2 W so that's the one shown below.

1. [**Raspberry Pi Zero 2 W board with header attached**](https://www.pishop.us/product/raspberry-pi-zero-2-w-with-pre-soldered-headers/) from PiShop.us or other.  If you don't have a power supply you'll want that also and a heat sink.  Use the options on the PiShop.us page for selecting the power supply and heatsink if desired.
2. MMDVM Hat and case.  Amazon is a good source for the HAT (Hardware Attached on Top). Here are 2 options:
	1. [**Upgraded MMDVM Hotspot HAT Board**](https://www.amazon.com/gp/product/B0C3J64TVD/ref=ewc_pr_img_1?smid=A111RPS%20MN20VWK&psc=1) (includes an 8 MB Micro SD card with Pi-Star ver 4.2.X pre-loaded.  You'll need to reflash to WPSD. The photo on the Amazon page shows the Micro SD card to be a Class 10)
	2. [**AUSINC MMDVM with enclosure**](https://www.amazon.com/gp/product/B07Z8YP5VJ/ref=ewc_pr_img_2?smid=A3KC9Z86+M9XWS3) (Micro SD card not included)
3.	Micro SD card if your MMDVM does not come with one. A high quality Class 10 Micro SD card is preferred, like the [**SanDisk Ultra**](https://www.amazon.com/SanDisk-Ultra-UHS-I-Memory-Adapter/dp/B00M55C0NS/ref=sr_1_18?s=pc&sr=1-18). 
4.	For powering the hotspot for mobile or portable operation a vehicle USB port or power bank (e.g. RAVPOWER) with USB port.

### Download required software and setup:

Download [**Pi-Star**](https://www.pistar.uk/downloads/) and follow their instructions for installing and configuring the software.

If using WPSD, follow the [**WPSD Instructions.**](https://w0chp.radio/wpsd/)

### Write the downloaded s/w to the MicroSD card

Download [**Balena Etcher**](https://etcher.balena.io/)[^14] to write the s/w to the SD card.  

On the Pi-Star website choose Pi-Star tools menu then the wifi builder to enter your SSID and password. 

Follow the instructions on the site to continue the install.

After the intitial install and reboot, run the Update from the Admin menu.

Have fun!  


## <span style="color: blue">Helpful Digital Voice links</span>

- [**W0CHP Digital Ham Radio Lists**](https://w0chp.radio/digital-radio-lists/) Chip, W0CHP, updates his searchable lists hourly.  Very useful. 

- [**DMR Unification Project**](https://dmrup.org/) A good read for understanding DMR and DMR network options, particularly the video shown on the main page of the website.

- [**D-STAR Repeater List**](https://dstarusers.org/repeaters.php)

- [**D-STAR Lastheard**](https://dstarusers.org/lastheard.php) - useful for checking if you or others are actually on the D-STAR system

- [**The Simple Guide to using D-STAR Radio**](https://tinyurl.com/bd5nak9v)

- [**Amateur Radio Guide to Digital Mobile Radio**](http://dmr-marc.net/media/Amateur_Radio_Guide_to_DMR_Rev_I_20150510.pdf)

<pre></pre>

[back to Dashboard](http://xlx517.radiosc.net/index.php)


[^1]: A Raspberry Pi (RPi) is a small computer that can be configured for multiple uses including as a desktop computer.  For KR4CHS, the RPi is used to run the IcomGateway software by Thomas Early, N7TAE.
[^2]: The IcomGateway provides access to multiple reflector types.
[^3]: Transcoding involves converting digital transmissions from one mode to others (e.g. D-STAR to DMR and YSF). So transcoding allows QSOs for operators using different modes.
[^4]: D-STAR - Digital Smart Technologies for Amateur Radio. Per [**Icom**](https://www.icomjapan.com/explore/d-star/), D-STAR is an open protocol for digital communications established by the Japen Amateure Radio League (JARL). For more on D-STAR see [**Diving into D-STAR**](https://amateurradionotes.com/d-star.htm).
[^5]: DMR - Digital Mobile Radio. Per the Motorola Solutions website, DMR is an international standard for two-way radios.  The standard was created and is maintained by the European Telecommunications Standards Institute (ETSI). DMR is characterized by the use of two Time Slots which allows for two QSOs to occur on a frequency. For more on DMR see [**Discovering DMR**](https://amateurradionotes.com/dmr.htm) and the [**DMR Association**](https://www.dmrassociation.org/).
[^6]: YSF or Yaesu System Fusion.  YSF is Yaesu's digital communications product for voice and data.  For more information read Yaesu's [**Invitation to the Future**](https://yaesu.com/pdf/System_Fusion_text.pdf).
[^9]: Talk Groups are a way for groups of users to share a time slot (one-to-many) without distracting and disrupting other users of the time slot. It should be noted that only one Talk Group can be using a time slot at a time. If your radio is not programmed to listen to a Talk Group, you will not hear that group’s traffic. There are over 16-million TGs available in DMR, most use only a very few (Amateur Radio Guide to Digital Mobile Radio, 2nd Edition).
[^8]: Reflectors are a type of network server, and you can think of their modules as chat rooms.
[^10]: A YSF Room is similar to a D-STAR Reflector and module and allows QSOs between YSF operators in the same room. 
[^11]: Gateway in this context refers to the D-STAR Gateway which connects operators through the Internet.
[^12]: An Amateur Radio Hotspot functions as a "private repeater" for the operator that provides access to Talkgroups, Reflectors, Chat Rooms, etc.
[^13]: A DMR Zone is a group of one or more channels.  A channel must be in a zone in order for it to be used.
[^14]: Balena Etcher is a software utility that flashes (copies) Operating System images to SD cards and USB drive.
[^7]: M17 is an Open Source digital voice mode.  For more information see the [**M17 Project**](https://m17project.org/).
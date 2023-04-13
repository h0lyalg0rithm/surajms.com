---
author: h0lyalg0rithm
comments: true
date: 2014-08-05 19:13:02+00:00
layout: post
link: http://surajms.com/2014/08/unbricking-tp-link-mr3020/
slug: unbricking-tp-link-mr3020
title: Unbricking my TP-link MR3020
wordpress_id: 125
categories:
- Hardware
- Mips
---

Two nights ago I accidentally bricked my router by flashing the original firmware over openWRT firmware on the MR3020.


**WARNING:If you want to flash the original firmware remove the boot part from the firmware.**


After quick google, I came across this [page](http://wiki.openwrt.org/toh/tp-link/tl-mr3020).It was had all of the instructions i needed to fix my bricked router. Unfortunately it required some extra hardware especially a usb to serial convertor, soldering iron and some headers.It had been more than 1 year that i soldered anything(Last time being in college).I had the necessary resistors leftover from my arduino project.

I took apart the router and found out the necessary pins for the header.Now it was time to solder.Moreover the openWRT website also had the pin layout with the necessary details of the pins.




<table class="inline" >
<tbody >
<tr class="row0" >
1
2
3
4
</tr>
<tr class="row1" >

<td colspan="1" rowspan="1" class="col0" >TX
</td>

<td colspan="1" rowspan="1" class="col1" >RX
</td>

<td colspan="1" rowspan="1" class="col2" >GND
</td>

<td colspan="1" rowspan="1" class="col3" >VCC
</td>
</tr>
</tbody>
</table>


All I had to do was connect the 10K resistor from the TX pin to the VCC pin.The connection to the usb device was also simple.
RX -> TX
TX -> RX
GRND -> GRND

[![MR3020](/wp-contents/uploads/2014/08/mr3020.jpg)](/wp-contents/uploads/2014/08/mr3020.jpg)

[![IMG_0778](/wp-contents/uploads/2014/08/IMG_0778.jpg)](/wp-contents/uploads/2014/08/IMG_0778.jpg)

[![IMG_0779](/wp-contents/uploads/2014/08/IMG_0779-1024x975.jpg)](/wp-contents/uploads/2014/08/IMG_0779.jpg)

Time to flash the firmware.I had to run a tftpd server on my machine and a serial connection to the device.I tried running the device at 56000 bits.It didnt work all gibberish on the screen.After the reading the instructions again.I had to set the bit rate to about 115200.Once that was done.The text was legible.Once the autobooting text came up on the screen I had to type **tpl**(Note sure why but that was some sort of 'open sesame' for the bootloader developers).Then i ran the following commands.

    
    hornet> setenv ipaddr 192.168.1.1
    hornet> setenv serverip 192.168.1.2
    hornet> tftpboot 0x80000000 openwrt-ar71xx-generic-tl-mr3020-v1-squashfs-factory.bin
    eth1 link down
    dup 1 speed 100
    Using eth0 device
    TFTP from server 192.168.1.2; our IP address is 192.168.1.1
    Filename 'openwrt-ar71xx-generic-tl-mr3020-v1-squashfs-factory.bin'.
    Load address: 0x80000000
    Loading: #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             #################################################################
             ######################################################
    done
    Bytes transferred = 3932160 (3c0000 hex)
    hornet> erase 0x9f020000 +0x3c0000
    
    First 0x2 last 0x3d sector size 0x10000                                                                                                        61
    Erased 60 sectors
    hornet> cp.b 0x80000000 0x9f020000 0x3c0000
    Copy to Flash... write addr: 9f020000
    
    done
    hornet> bootm 9f020000




Once this was done the router was back from the dead ready for some more tweaking.

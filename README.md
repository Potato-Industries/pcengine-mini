# pcengine-mini

Some rough notes on getting root and FEL mode on the PCEngine Mini (i couldn't easily find anything online).

Ref:

https://honeylab.hatenablog.jp/entry/2020/03/21/224924 (great work, must read)


# root

Hook up UART pins as documented in the blog above.

```
screen /dev/ttyUSB0 115200
```

Power on device spam 's' key on screen console.

Getting root shell via uboot console.

```
sunxi#setenv init /bin/sh
sunxi#boot
## Booting kernel from Legacy Image at 43800000 ...
   Image Name:   Linux-3.4.113
   Image Type:   ARM Linux Kernel Image (uncompressed)
   Data Size:    3485072 Bytes = 3.3 MiB
   Load Address: 40008000
   Entry Point:  40008000
   Verifying Checksum ... OK
   Loading Kernel Image ... OK
OK
para err in disp_ioctl, cmd = 0xa,screen id = 1
[     18.397][mmc]: mmc exit start
[     18.402][mmc]: mmc_config_clock: clk 50000000
[     18.406][mmc]: mmc_config_clock: clk 400000
[     18.421][mmc]: mmc 2 cmd 8 err 100
[     18.427][mmc]: mmc send if cond failed
[     18.432][mmc]: mmc 2 cmd 55 err 100
[     18.438][mmc]: send app cmd failed
[     18.452][mmc]: get sdc_phy_wipe fail.
[     18.456][mmc]: get sdc0 sdc_erase fail.
[     18.460][mmc]: get sdc_2xmode ok, val = 1
[     18.464][mmc]: get sdc_ddrmode ok, val = 1
[     18.468][mmc]: get sdc_f_max fail,use default  50000000Hz
[     18.474][mmc]: get card_line ok, card_line = 8
[     18.478][mmc]: get sdc_ex_dly_used fail,use default
[     18.483][mmc]: mmc 2 exit ok
[     18.486]
Starting kernel ...

Uncompressing Linux... done, booting the kernel.
<6/bin/sh: can't access tty; job control turned off
/ # id
uid=0(root) gid=0(root)
/ # passwd
Changing password for root
New password: 
Bad password: too short
Retype password: 
Password for root changed by root
```

Power cycle the device, you are good to go, passwd changes are persisted. 

```
/ # �[      0.203]

U-Boot 2011.09-rc1-00000-g481c142-dirty (Sep 26 2019 - 00:36:30) Allwinner Technology 

[      0.213]version: 1.1.0
[      0.215]uboot commit : 481c1423f323257356c9db28e780864137596a70
 
ready
normal dc exist, limit to dc
no key input
dram_para_set start
dram_para_set end
In:    Out:   Err:   Net:   Warning: failed to set MAC address

IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0
IRQ: EP0

   Verifying Checksum ... OK
OK
OK
Uncompressing Linux... done, booting the kernel.
/dev/by-name/UDISK: UUID="beca5410-23bf-4c4a-8702-8d8319d61e01" TYPE="ext4"
/dev/by-name/UDISK already format by ext4
/dev/by-name/rootfs_data: UUID="0de2d00c-f534-419e-b090-368fdb0ae7da" TYPE="ext4"
/dev/by-name/rootfs_data already format by ext4
/dev/by-name/app: UUID="e5969eed-c0e7-40cd-a7fa-972b2ab43660" TYPE="ext4"
/dev/by-name/app already format by ext4
/dev/by-name/misc: UUID="e789e63c-e47f-4f36-8332-b6ef5143cc7d" TYPE="ext4"
/dev/by-name/misc already format by ext4
release-indiana-da99667:INDIANA-mass
Starting logging: OK
Populating /dev using udev: done
read-only file system detected...done
mali: starting driver
mode: 0
automatic mode: display don't support 720p and 480p. 720p mode selected
OK
User Mode:[gpio-keys] Does not verify vid and pid
[joypad-1] device: /dev/input/by-path/platform-sunxi-ehci.1-usb-0:1.2:1.0-event-joystick does not exists.
start game.
start game.
value is: 0

170

Welcome to VividOS
VIVID login: root
Password: 
# id
uid=0(root) gid=0(root) groups=0(root),10(wheel)

```


# FEL Mode

Spam '2' key while powering up the device via usb. 

```
wopr-re# sunxi-fel -l
USB device 002:034   Allwinner A33     0461872a:89046009:aa96c787:6c118000
```


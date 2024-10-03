# Alpine XFCE4 desktop setup
===========================================================

This is a single only full article for first users, 
targeted for mid-impatient that just want the way to see the desktoip in some hours:

If you are impatient: [.. use this guide named Fast Forward XFCE desktop](../tutorials/alpine-tutorial-desktop-xfce4-fast-forward.md)
If you want wayland crap: [.. use this guide named Fast Forward Wayland desktop](../tutorials/alpine-tutorial-desktop-wayland-try.md)

* [How to use this guide](#how-to-use-this-guide)
* [Installation of alpine](#installation-of-alpine)
    * [Fast explanations, just 5 lines](#explanations)
    * [how to install in single disc only](#how-to-install-in-single-disc-only)
* [preparation](#preparation-xfce4-aline)
    * [instalation](#instalation)
    * [setup OS configuration](#setup-os-configuration)
    * [configuration programs and repositories](#configuration-programs-and-repositories)
    * [setup system users](#setup-system-users)
    * [setup hardware media support and graphical subsystem](#setup-hardware-media-support-and-graphical-subsystem)
    * [setup software graphical fonts and languajes](#setup-software-graphical-fonts-and-languajes)
    * [setup hardware media support and sound subsystem](#setup-hardware-media-support-and-sound-subsystem)
* [Instalacion XFCE4 Alpine](#instalacion-xfce4-apine)
* [Desktop multimedia and media devices](#desktop-multimedia-and-media-devices)
* [Desktop Office suite](#desktop-office-suite)
* [Development](#development)
    * [base console development](#base-console-development)
    * [base gui development](#base-gui-development)
* [Licensing clarifications](#licensing-clarifications)
* [See also](#see-also)

## How to use this guide

This guide **structure all the commands in blocks, each block its separated by a line spaced**, 
so you must **tipe each line as is.. and hit enter**, but if you are in gui or remotelly just do:

1. copy each separated by empty line, block of command, copy only blocks separate by empty line
2. and paste each separated by empty line block in the remnote (ssh), do not paste all the blocks at same time!

**If you have another computer or gui**, try to use SSH client like putty or just in terminal (MAC or Linux) do:

1. at the Alpine installation: `sed -i 's|.*PermitRootLogin.*|PermitRootLogin yes|g' /etc/ssh/sshd_config;service sshd restart`
2. at the other OS just connect: `ssh -l root <ip>` change "`<ip>`" with the address of your device.
3  after finish, rerun: `sed -i -r 's|.*PermitRootLogin.*|PermitRootLogin no|g' /etc/ssh/sshd_config;service sshd restart`

> **Warning** Some Linux or/and Mac terminals have security cut/paste locks, so 
if you paste, the first line will be preceded by garbage, check always the first char of your paste.

## Installation of alpine

This guide will assume all the hard disk storage for the installation 
otherwise check the best option at [alpine-newbie-install.md](alpine-newbie-install.md)

Ok but if you are impatient: [.. use this guide named Fast Forward XFCE desktop](../tutorials/alpine-tutorial-desktop-xfce4-fast-forward.md)

#### Explanations

Alpine is the OS (Operating System), that runs on your machine. 
Programs such as a web browser runs on the OS, and web pages like 
this are handled by the web browser.

About desktop? alpine is the Program combo that really runs in dockers, 
because of that, the desktop part its not so targeted and focused.. 
Linux is just the kernel that handles and manages the hardware to the operating system

#### how to install in single disc only

* **1** download the image of the alpine ISO
    * i386 older 32bit use : http://dl-cdn.alpinelinux.org/alpine/v3.12/releases/x86_64/alpine-extended-3.12.0_rc1-x86.iso
    * amd64 newer 64bit use : http://dl-cdn.alpinelinux.org/alpine/v3.19/releases/x86_64/alpine-extended-3.19.0_rc1-x86_64.iso
    * amrv7 or 64bit old use : http://dl-cdn.alpinelinux.org/alpine/v3.16/releases/armv7/alpine-standard-3.16.0_rc1-armv7.iso
    * amrv8 or 64bit newers : http://dl-cdn.alpinelinux.org/alpine/v3.19/releases/aarch64/alpine-standard-3.19.1-aarch64.iso
* **2** dump into usb stick.. check the process to do here: [alpine-newbie-how-to-dumb-easyle-with-gui-to-usb.md](alpine-newbie-how-to-dumb-easyle-with-gui-to-usb.md)
* **3** boot the usb stick from your computer.. this will depend of your vendor
* **4** after boot, just login.. using "root" word
* **5** type "setup-disk" and start to answer the first two questions, keyboard type and layout
* **6** Keyboard Layout (Local keyboard language and usage mode, e.g. us and variant of us-nodeadkeys.)
* **7** Hostname (The name for the computer.) Please here dont put symbols, and use a 8 chars only name.
* **8** Network (For example, automatic IP address discovery with the "DHCP" protocol.) for hoe just use "dhcp"
* **9** DNS Servers (Domain Name Servers to query. just use google's 8.8.8.8 .)
* **10** Timezone, becouse this is a single install just use UTC
* **11** Proxy (Use "none" for direct connections to the internet.)
* **12** Mirror (From where to download packages. Here put 1 and later we will tune up)
* **13** SSH (Secure SHell remote access server, mandatory, "Openssh" is part of the default install image)
* **14** NTP (Network Time Protocol client used for keeping the system clock in sync with a time server. "chrony")
* **15** Disk Mode here just select the sys mode, we are installing to use as desktop in single disc, so all the data will be wiped and erased.

If you must tune up we recommended to use virtual machine or check the best option at [alpine-newbie-install.md](alpine-newbie-install.md)

All the 15 steps are the description of the installation process when you run `setup-alpine`

## preparation Xfce4 Alpine

To have a usable desktop without having to wonder why it doesn't sound, 
or why the video file doesn't display, **you should avoid minimalisms if 
you don't already have advanced knowledge** of alpine and even more so of linux.

#### Internet required or offile iso

If you dont have wired internet connection, check [lack of wireless setup](#lack-of-wireless-setup) section of this document.

**Or just please use our direct VenenuX Alpine ISOS**
[CURRENT LINK https://t.me/alpine_linux/762, but ask in telegram alpine network for newer one](https://t.me/s/alpine_linux/762)

#### setup OS configuration

Runs following commands as root user:

1. deny access to the ssh root user, or well, get sure to deny such access
2. setup and start the ssh service, this always be present in Alpine installs
3. set the name of the computer, here we used `venenux-desktop`, please avoid symbols
4. setup services of network to init at boot check [differences of hard coded setup](#differences-of-hard-coded-setup) section of this document
5. configure root account and update repositories
6. add the CSH shell and enable it using community repositories
7. create a remote connection limited account `daru`, check [the daru user explanation](#the-daru-user-explanation) section of this document
8. configure a default remote connection account `daru` as standard

```
sed -i -r 's|#PermitRootLogin.*|PermitRootLogin no|g' /etc/ssh/sshd_config

service sshd restart

rc-update add sshd default

hostname venenux-desktop
echo 'hostname="venenux-desktop"' > /etc/conf.d/hostname 
echo "venenux-desktop" > /etc/hostname

rc-update add networking boot

cat > /root/.cshrc << EOF
unsetenv DISPLAY || true
HISTCONTROL=ignoreboth
EOF
cp /root/.cshrc  /root/.bashrc  /root/.profile
 echo "root:toor" | chpasswd

cat > /etc/apk/repositories << EOF
http://dl-4.alpinelinux.org/alpine/v$(cat /etc/alpine-release | cut -d'.' -f1,2)/main
http://dl-4.alpinelinux.org/alpine/v$(cat /etc/alpine-release | cut -d'.' -f1,2)/community
EOF
apk update

apk add tcsh && add-shell '/bin/csh'

adduser -D -g "" -u 998 -h /opt/daru -s /bin/csh daru

 echo "daru:daru" | chpasswd

rm -f /opt/daru/*

mkdir /opt/daru

cat > /opt/daru/.cshrc << EOF
unsetenv DISPLAY
export PAGER=less
set autologout = 6
set prompt = "$ "
set history = 0
set ignoreeof
EOF
cp /opt/daru/.cshrc /opt/daru/.bashrc
```

Those command put your alpine in "minimal user mode" so means only one user will 
be able to login from remote using ssh, the normal user will be "general", but
for more info of `daru`, check [the daru user explanation](#the-daru-user-explanation) 
section of this document

Next section will cover the suser management and programs support:

include(alpine-newbie-shells.md)

#### configuration programs and repositories

This will convert and configures your alpine installation into a more close 
and working linux operating system, you will have:
* manpages will be available, so you can check the operating system and gnu documetation
* commands will work exactly as another linxu or mac, google results of your doubs will work
* will provide elevation protected for users and minimize the confortability of root account
* will provide all the system tools to the devices management
The following commands are separated by sections (check [How to use this guide](#how-to-use-this-guide) ).

1. Setup main and community repositories of sources of programs and update it
2. install most common shell and command line manager
3. install main command line utilities, man page and easy to use editor
4. install string manipulation tools for the commands on the console
5. install file downloaders and url handlers for command line administration
6. install support for backend of basic archivers and file manipulation
7. install extra archiving tools and file manipulation tools
8. add support for languaje environment and timezone
9. install device information support and console management


``` bash
cat > /etc/apk/repositories << EOF
http://dl-4.alpinelinux.org/alpine/v$(cat /etc/alpine-release | cut -d'.' -f1,2)/main
http://dl-4.alpinelinux.org/alpine/v$(cat /etc/alpine-release | cut -d'.' -f1,2)/community
EOF
apk update

apk add bash bash-doc bash-dev bash-completion readline readline-doc dialog dialog-doc

apk add coreutils coreutils-doc mandoc man-pages nano nano-doc binutils binutils-doc

apk add sed sed-doc lsof lsof-doc less less-doc groff groff-doc gawk gawk-doc

apk add wget wget-doc curl curl-doc aria2 aria2-doc

apk add zip zip-doc p7zip p7zip-doc xz xz-doc tar tar-doc lha lha-doc attr attr-doc cpio cpio-doc lha lha-doc lz4 lz4-libs lz4-doc lz4-static

apk add file file-doc arch-install-scripts arch-install-scripts-doc tree tree-doc apk add e2fsprogs e2fsprogs-doc btrfs-progs btrfs-progs-doc exfat-utils f2fs-tools f2fs-tools-doc dosfstools dosfstools-doc xfsprogs xfsprogs-doc jfsutils jfsutils-doc

apk add musl-locales musl-locales-lang tzdata tzdata-utils terminus-font

apk add pciutils pciutils-doc usbutils usbutils-doc lshw lshw-doc
```

The packages that have a "-doc" part handles the manpages.. you can 
avoid those packages, if Alpine usage will be for GUI only or minimal setup.

The packages of locales will be need as base for multi-lang enviroment.

If you are impatient: [.. use this guide named Fast Forward XFCE desktop](../tutorials/alpine-tutorial-desktop-xfce4-fast-forward.md)

#### setup system users

Now we need an user, to use the system, the `root` account only will do delicate 
or administrative task, **you never use anything under root unless setup things!**
and you must to avoid any user elevation command, always run `su` for that!

We will follow a protocol for better identification of all the commands 
in further documents, the user will be called "general"; this is important 
that it has does matter, what does not matter is for you cos you only "use".

The other important part here is the groups, user will not have proper access 
to resources because the OS manages the access using levels by groups. Of course 
all of this only works using the proper policy kit software.

1. install and setup advanced management of users and administration tool privilegies
2. setup the shell csh for all present users and future ones
3. setup the shell bash for all present users and future ones
4. setup the shell for skel directory, that will server as template
5. setup the Xresources configuration for skel directory, that will server as template
6. configure defaults for each new creation of new users with bash as default shell
7. configure the login environement for each user when login at the console
8. create the default new general usage user `general` for your desktop or console daily work
9. include this `general` user in the most used need groups to have proper access to resources

```
apk add shadow shadow-doc shadow-uidmap doas doas-doc doas-sudo-shim

cat > /tmp/tmpcs.tmp << EOF
set history = 10000
set prompt = "$ "
EOF

for i in $(ls /home);do cat /tmp/tmpcs.tmp > /home/$i/.cshrc;done

cat > /tmp/tmpbs.tmp << EOF
set prompt = "$ "
set history = 10000
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
EOF

for i in $(ls /home);do cat /tmp/tmpbs.tmp > /home/$i/.bashrc;done

mkdir /etc/skel
cat /tmp/tmpcs.tmp > /etc/skel/.cshrc
cat /tmp/tmpbs.tmp > /etc/skel/.bashrc

cat > /etc/skel/.Xresources << EOF
Xft.antialias: 0
Xft.rgba:      rgb
Xft.autohint:  0
Xft.hinting:   1
Xft.hintstyle: hintslight
EOF

cat > /etc/default/useradd << EOF
# useradd defaults file
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
EOF

cat > /etc/login.defs << EOF
USERGROUPS_ENAB yes
LOG_OK_LOGINS		no
SYSLOG_SU_ENAB		yes
SYSLOG_SG_ENAB		yes
SULOG_FILE	/var/log/sulog
SU_NAME		su
ENV_SUPATH	PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV_PATH	PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
UMASK		022
UID_MIN			 1000
UID_MAX			60000
SYS_UID_MIN		  100
SYS_UID_MAX		  999
GID_MIN			 1000
GID_MAX			60000
SYS_GID_MIN		  100
SYS_GID_MAX		  999
LOGIN_RETRIES		3
LOGIN_TIMEOUT		60
CONSOLE_GROUPS		floppy:audio:cdrom:users
EOF


useradd -m -U -c "" -G wheel,input,disk,floppy,cdrom,dialout,audio,video,lp,netdev,games,users,ping general

for u in $(ls /home); do for g in disk lp floppy audio cdrom dialout video lp netdev games users ping; do addgroup $u $g; done;done
```

In the last part the `general` user is created since for purposes of usage 
the name its hard coded for the commands that can be sense and important, 
because of the references in further documents.

At last, the groups are cofigured for the user, each one will define a 
resource access, specially those for `disk`, `audio`, `video` and `netdev`.

#### setup hardware media support and graphical subsystem

Until this point, we have a user that can login to the system, 
and bunch of programs to interact with the OS, but still do not 
have any programs to make the computer or device work for us.. 
this target depends of the set of programs, this section will 
configure the graphical environment to property setup any desktop.

1. install programs to manage devices dinamically by the OS and not admin user
2. setup service for dynamic device manager at boot, energy management and cpu frecuency management
3. install the graphical subsystem and modesetting multi GPU video card support
4. install the programs that manages the 3D backend for graphics
5. install set of need modules for basic GPU and dummy ones like virtual machines, avoid if not need.
6. install set of need modules for 2D/3D specific GPU or video card not so older generation supported
7. install set of need modules for 2D/3D common GPU or video card almost modern still supported
8. install support for multi resolution and keyboard language configuration over GUI programs
9. install the bus communitacion support, policy management and login backend and frontend
10. generate the machine id identification hack for stupid shistemd linux standards
11. activate the service of the bus cominucations, the policy rules and graphical login backend
12. start the service of the bus cominucations, the policy rules and graphical login backend
13. activate the service of the graphical frontend login manager
14. start the service of the graphical frontend login manager
15. install support for abstract device filesystem representation using FUSE user space
16. activate the service of abstract device filesystem representation using FUSE user space
17. install software backend for usage of abstract device filesystem representation using FUSE user space

```
apk add acpi alpine-conf eudev eudev-doc eudev-rule-generator eudev-openrc linux-firmware cpufreqd pciutils util-linux zram-init

modprobe fbcon && echo "fbcon" >> /etc/modprobe
setup-devd udev

rc-update add udev
rc-update add acpid
rc-update add cpufreqd

apk add xorg-server xorg-server-xnest xorg-server-doc xf86-video-modesetting xf86-input-libinput freeglut glew glu

apk add mesa mesa-gl mesa-utils mesa-osmesa mesa-egl mesa-gles mesa-dri-gallium mesa-va-gallium libva-intel-driver intel-media-driver

apk add xf86-video-dummy xf86-video-vesa xf86-video-qxl xf86-input-evdev xf86-input-synaptics

apk add xf86-video-apm xf86-video-openchrome xf86-video-r128 xf86-video-sis

apk add xf86-video-i128 xf86-video-i740 xf86-video-savage xf86-video-s3virge xf86-video-chips xf86-video-tdfx

apk add xf86-video-ast xf86-video-rendition xf86-video-ark xf86-video-siliconmotion xf86-video-fbdev

apk add xf86-video-amdgpu xf86-video-nouveau xf86-video-intel xf86-video-vmware xf86-video-ati xf86-video-nv

apk add linux-firmware-amdgpu linux-firmware-radeon linux-firmware-nvidia linux-firmware-i915 linux-firmware-intel

apk add libxinerama xrandr kbd setxkbmap xinit xf86-input-evdev

apk add dbus dbus-x11 elogind elogind-openrc elogind-lang polkit polkit-openrc polkit-elogind lightdm lightdm-lang lightdm-gtk-greeter 

dbus-uuidgen > /var/lib/dbus/machine-id

rc-update add dbus
rc-update add elogind
rc-update add polkit

rc-service dbus restart

rc-service elogind restart

rc-service polkit restart

rc-update add lightdm

rc-service lightdm restart

apk add fuse fuse-exfat-utils archivemount fuse-exfat avfs vte3 pcre2

rc-service fuse start

rc-update add fuse

apk add gvfs udisks2 udisks2-lang udisks2-doc gvfs-fuse gvfs-archive gvfs-dav gvfs-nfs gvfs-lang
```

If you are impatient: [.. use this guide named Fast Forward XFCE desktop](../tutorials/alpine-tutorial-desktop-xfce4-fast-forward.md)

#### setup software graphical fonts and languajes

Now we have support for graphics in the operating system, 
but still do not have any graphical program, so we will prepare
minimal set of software for the right working of the programs 
such like the fonts and the support of multi languajes.

1. install console support fonts for tty terminal and console terminal programs
2. setup and configure the default tty terminal fonts
3. set as service the configuration of the font at terminal
4. install basic set of default fonts for graphical programs, dejavu and bitstream ones
5. install fonts for japanese symbos and sans/comic like fonts
6. install fonts for cyrillic langs to display russian words
7. install fonts for mid-orient langs like arabic, hebrew, armenian, hindi / sanskrit
8. install fonts for langs like tailan and  malayalam
9. install fonts for east-orient like chinese symbols,hangul and kana ones, includign japanese

```
apk add terminus-font

setfont /usr/share/consolefonts/ter-132n.psf.gz

sed -i "s#.*consolefont.*=.*#consolefont="ter-132n.psf.gz"#g" /etc/conf.d/consolefont

rc-update add consolefont boot

apk add ttf-dejavu font-bitstream-type1 font-bitstream-100dpi font-bitstream-75dpi font-adobe-utopia-type1 font-adobe-utopia-75dpi font-adobe-utopia-100dpi font-noto-georgian

apk add font-noto font-noto-extra font-noto-cjk font-noto-cjk-extra font-arabic-misc ttf-liberation ttf-linux-libertine 

apk add font-misc-cyrillic font-mutt-misc font-screen-cyrillic font-winitzki-cyrillic font-cronyx-cyrillic

apk add font-noto-hebrew font-noto-arabic font-noto-armenian font-noto-cherokee font-noto-devanagari font-noto-ethiopic

apk add font-noto-lao font-noto-malayalam font-noto-tamil font-noto-thaana font-noto-thai

apk add font-noto-cjk font-noto-cjk-extra font-isas-misc
```

If you want to bypass and dont know anything, run steps from 1 to 4 adn then 
after step 4 just install `font-noto-all` that provides support for all 
langs symbols words.

#### setup hardware media support and sound subsystem

Audio support these days depends on video support, although it can still be 
configured separately, nowadays it is strongly tied to video, that's why its 
placed here this section, just below of the hardware video setup.

It should be noted that in Linux there is the system audio layer and the user audio layer, 
formerly the first was and can used directly, nomadays, by using the second 
we are in transition to the wonderful pipewire framework.

1. install the base audio subsystem software
2. install the base audio framework user support
3. set alsa to start on each boot
4. restart bus communicacion, due we already have the software video subsystem support bus communication
5. setup the mixed volumes, becous comes muted
6. setup the access prority for the audio communication and pipewrite also
7. install optional bluetooth software support if you have a bluez audio card or phones
8. setup the bluetooth service
9. start the bluetooth service so the audio devices can be stablished

```
apk add alsa-utils alsa-utils-doc alsa-plugins alsa-plugins-doc alsa-tools alsa-tools-doc alsaconf linux-pam

apk add pipewire pipewire-doc pipewire-pulse pipewire-alsa pipewire-jack sndio sndio-doc wireplumber-logind

rc-update add alsa

rc-service dbus restart

amixer sset Master unmute;
amixer sset PCM unmute;
amixer set Master 100%;
amixer set PCM 100%;

cat > /etc/security/limits.d/audio-limits.conf << EOF
@audio - memlock 4096
@audio - nice -11
@audio - rtprio 88
@pipewire - memlock 4194304
@pipewire - nice -19
@pipewire - rtprio 95
EOF

apk add bluez bluez-deprecated bluez-openrc pipewire-spa-bluez
modprobe btusb && echo "btusb" >> /etc/modprobe
rc-update add bluetooth

rc-service bluetooth start
```

Now at this point we have audio and video configured, additionally we have 
basic support for managing devices dynamically when connecting or disconnecting, 
the only kind of devices not covered yet until this point are printers.

For any desktop this is the point where you choose which graphical environment 
or desktop to install. Next section will prefers the XFCE4 desktop setup, 
currently ws the first and its the most complete desktop packaged in the repos.

> **Warning**: pipewire needs `XDG_RUNTIME_DIR` configured correctly, if not `~/pulse` will be created and **pavucontrol** willnot access to!

##### pipewire running without graphical session

This means **no dbus** and no `XDG_RUNTIME_DIR` setup, the pipewrite can 
be configured to assumed never will exits a graphical session running, 
also the package `eudev` must be installed for alsa cards.

This method is not sure to work in almost all cases, so if fails just leave only alsa packages and setup alsa only!

```
cp -a /usr/share/pipewire /etc

cp -a /usr/share/wireplumber /etc

sed -i 's|.*support.dbus.* =.*|    support.dbus = false|g' /etc/pipewire/pipewire.conf
sed -i 's|.*support.dbus.* =.*|    support.dbus = false|g' /etc/wireplumber/wireplumber.conf
sed -i 's|.*\["with-logind"\].*=.*|  ["with-logind"] = false|g' /etc/wireplumber/bluetooth.lua.d/50-bluez-config.lua
sed -i 's|.*\["alsa.reserve"\].*=.*|  ["alsa.reserve"] = false|g' /etc/wireplumber/main.lua.d/50-alsa-config.lua
```

**Only do this if you never will run a managed xdg sesion or x11/wayshit setup**, of 
course this also will need the `linux-pam` and `pipewire` packages, becouse the second 
does not depends on the first so will fails if you dont installed xplicit!

**PROBLEMS**: if you try to run any alsa or app and get "Host is down", means that 
the pipewire session and the access is wronly configured. try "alsamixer -c0" to 
check if work or `alsamixer -c1` or similar, and if work the pipewire session 
must be reconfigured to provide media device access, try to added the user to the 
group of pipewire.


## instalacion Xfce4 Alpine

Since Alpine 3.13 the XFCE4 desktop its full modern, this means its pretty more heavy, 
cos is build using GTK3 only.

On older or cheap devices, mostly for 32bit devices its better to use alpine 3.10 or 3.12 
that uses GTK2 for almost all the programs.

1. install base desktop software packages
2. install base XFCE4 desktop packages, at this point, the system its ready for graphicall session
3. install and setup the login manager programs and policy manager software
4. setup the display login manager to start at boot
5. start the display manager, now you can use a minimal XFCE4 desktop, continue for complete experience
6. install cliboard manager, keyboard configurator, screensaver, screenshooter, and baterry manager
7. install packages for multi lang environment of the XFCE4 desktop if need, if login, logout and relogin

```
apk add gtk-update-icon-cache hicolor-icon-theme paper-gtk-theme adwaita-icon-theme mate-themes

apk add xfce4 xfce4-session xfce4-panel xfce4-terminal xarchiver mousepad network-manager-applet xfwm4-themes xfce-polkit xfce4-skel xfce4-power-manager xfce4-settings

apk add lightdm elogind elogind-openrc elogind-lang polkit polkit-openrc polkit-elogind lightdm lightdm-lang lightdm-gtk-greeter 

rc-update add lightdm

rc-service lightdm restart

apk add xfce4-clipman-plugin xfce4-xkb-plugin xfce4-screensaver xfce4-screenshooter xfce4-taskmanager xfce4-whiskermenu-plugin xfce4-battery-plugin

apk add xfce4-panel-lang xfce4-clipman-plugin-lang xfce4-xkb-plugin-lang xfce4-screenshooter-lang xfce4-taskmanager-lang xfce4-whiskermenu-plugin-lang xfce4-battery-plugin-lang xfce4-power-manager-lang xfce4-settings-lang
 
```

The XFCE4 desktop is the most complete in Alpine, MATE and others have almost complete packages, 
with minor fails or missing. The newers LXQT and CoreCube desktops are made in QT technology 
so are more heavyweith for older devices, specially 32bit systems.

the LXDE desktop is not completed in alpine due the stupid mantainers policy of GTK3 targeted.

## Desktop multimedia and media devices


The media in linux its per se reduced, and in alpine so then more limited, 
with this lines you will have all the need suported, for converting and playing, 
and minimal support for editing.

1. install support for media management muti format over the programs
2. install support for sound and output of notifications over the programas
3. install support for media format reading and management backend (convertiion and reading)
4. install viewers for video and audio files
5. install management backend for media devices
6. install video resoulution flexibility and network backend support
7. install network frontend support and frontend management of network
8. install service task manager on boot
9. setup service of wifi backend management
10. setup general networking backend management service
11. setup all the users to property manage the audio, video and network devices
12. reconfigure the interfaces so the network gui can then manage it
13. start the network manager backend services, so the gui can manager then
14. at this point logout and relogin from your current sesion to start to work

```

apk add e2fsprogs e2fsprogs-doc btrfs-progs btrfs-progs-doc xfsprogs xfsprogs-doc \
 exfat-utils exfat-utils-doc f2fs-tools f2fs-tools-doc dosfstools dosfstools-doc \
 jfsutils jfsutils-doc parted parted-doc partimage partimage-doc testdisk testdisk-doc

apk add gst-plugins-base gst-plugins-bad gst-plugins-bad-lang gst-plugins-ugly gst-plugins-ugly-lang gst-plugins-good gst-plugins-good-gtk gst-plugin-pipewire

apk add libcanberra-gtk2 libcanberra-gtk3 libcanberra-gstreamer wxgtk-media wxgtk3-media wxgtk-lang pipewire-pulse pipewire-zeroconf pipewire-lang

apk add mediainfo ffmpeg ffmpeg-doc ffmpeg-libs lame lame-doc rtkit rtkit-doc 

apk add mpv mpv-doc deadbeef deadbeef-lang deadbeef-doc

apk add gvfs gvfs-fuse gvfs-archive gvfs-afp gvfs-afp gvfs-afc gvfs-cdda gvfs-gphoto2 gvfs-mtp pcmanfm blueman

apk add libxinerama xrandr wpa_supplicant dhcpcd chrony macchanger wireless-tools iputils

apk add network-manager-applet network-manager-applet-lang networkmanager networkmanager-lang networkmanager-elogind networkmanager-elogind-lang networkmanager-elogind-openrc networkmanager-openvpn networkmanager-openvpn-lang

rc-update add chrony

rc-update add wpa_supplicant

rc-update add networkmanager

for u in $(ls /home); do for g in plugdev audio cdrom dialout video netdev; do addgroup $u $g; done;done

cat > /etc/network/interfaces << EOF
auto lo
iface lo inet loopback
EOF

service networking restart

service wpa_supplicant restart

service networkmanager restart

```

## Desktop Office suite

In linux world there's no mayor suite or programs in such topic, 
just we need a reader (pdf, ebooks, cbr, zbr, etc) and office 
suite for word/calc processing (doc, xls, odt, ods, etc).


```
apk add libreoffice libreoffice-gnome evince evince-lang evince-doc
```

The programs will appear in the Office menu category.

##### differences of hard coded setup

Disk paths, Networks and WIFI in linux have two scopes, the system and the user, 
alpine uses a scope that is overwritten and superset if others apps are installed, 
like networkmanager or desktops is installed, therefore, the network configuration 
we make is temporary, and we assumed then wired one cos is easy to setup.

##### lack of wireless setup

WIFI networks are a little more complicated, that's why a wired network is assumed, 
if you don't have the possibility of having an internet network, simply use our 
complete iso that already has everything, and there you can use the wifi directly 
from the graphical desktop check [Internet required or offile iso](#internet-required-or-offile-iso) section.

##### the daru user explanation

The meaning of **"daru"** user is to **able to login to you from another computer by restrictions**.. 
so no one can login with other user.. daru have a restricted shell and restricted commands.

The **right way its to use SSH Key Pair and limited hosts, but that is so complicated for new users**, 
so using a restricted user for connections its enought untill that point.

Alpine **developers dont understand** that **normal users first wants to see the things working**, 
and later after understand the most relevenat for thems (desktop usage), 
users can setup others things.. 

## Licensing clarifications

**CC BY-NC-SA**: the project allows reusers to distribute, remix, adapt, and build upon the material 
in any medium or format for noncommercial purposes only, and only so long as attribution is given 
to the creators involved. If you remix, adapt, or build upon the material, you must license the modified 
material under identical terms,  includes the following elements:

* **BY**  – Credit must be given to the creator of each content respectivelly, starting at the first contributor.
* **NC**  – Only noncommercial uses of the work are permitted, with exceptions if you fill an issue here!
* **SA**  – Adaptations must be shared under the same terms, you must obey this terms and do not change it.

https://codeberg.org/alpine/alpine-wiki/src/branch/main#license

## See also

* [README.md](README.md)
* [alpine-newbie-install.md](alpine-newbie-install.md)
* [Fast Forward XFCE desktop](../tutorials/alpine-tutorial-desktop-xfce4-fast-forward.md)

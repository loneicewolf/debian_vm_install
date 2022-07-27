NOTE THIS IS NOT DONE

will be errors.




(In)secure Debian VM Install

- :warning:  (this guide will omit all the vm steps etc. it' will only include the OS install)
- `debian-11.4.0-amd64-netinst.iso`

**extremely simplified go trough**

boot it as **`BIOS`** - no UEFI(we already have QUBES OS as UEFI and CRYPTO), and we will not use any CRYPTO. But we will use LVM.

`; switch to a tty term and pre conf some stuff`


```

1 English, proper timezone
2 host name and dominate: `debvm1:lan`
3 user and group, pass: `op1:weak`

```


### manual disk: 
- **2 partitions**
- A  `1GB boot  (mount: '/boot', bootable flag on,)`
- B  `remaining space, ext4. `
- then do `config lvm`
  -  v group: `vg1`
  -  logical vols in `vg1`:
    - lswap (use as swap, 4GB)
    - lroot (`40GB`,  use as ext4, mount `/root/`)
    - lhome (`remaining space`,  use as ext4, mount `/home/`)


`=========================`


`*` *NO apt software. we don't want a bloated system. if we need/want a certain app, we can install it later(from source)*

`*` *No survey since this will be used insecurely, so we don't want to make misleading reports.*


### boot `1#`

#### Pre & Progress Info

```sh
# 1

date        >> DATE_BOOT_1
timedatectl >> DATE_BOOT_1

uname    >> UNAME_BOOT_1
uname -a >> UNAME_BOOT_1
uname -r >> UNAME_BOOT_1

df --human --all >> DF_BOOT_1
lsblk            >> LSBLK_BOOT_1

```



nano `APT_1.sh`

- **`note   if this is a kali vm (or if sec tools will be installed into it), kali-desk lxde for example. `**

```sh

echo "do not be root, use sudo"
echo "also ONLY RUN THIS ONCE"

sleep 5

apt autoremove
apt update
apt upgrade
apt autoremove
apt dist-upgrade
apt-get install upgrade-system
apt autoremove
apt autopurge

## pay attention here to what is being removed
## write that down.

apt remove telnet* netcat* openssh-server* openssh-client* firefox* deluge* audacious* smplayer* vlc* lxmusic* parcellite*
sudo apt autoremove

echo "reboot now and then MOVE THIS FILE TO  APT_1.DONE.txt"

```

`sudo bash APT_1.sh`

`reboot.`

`*` `mv (apt1 to apt1.done)`




### boot `2#`


#### Pre & Progress Info

```sh
# 2

date        >> DATE_BOOT_2
timedatectl >> DATE_BOOT_2

uname    >> UNAME_BOOT_2
uname -a >> UNAME_BOOT_2
uname -r >> UNAME_BOOT_2

df --human --all >> DF_BOOT_2
lsblk            >> LSBLK_BOOT_2

```




`nano APT_2.sh`

```sh

echo "do not be root, use sudo"
echo "also ONLY RUN THIS ONCE"

sleep 5

## pay attention here to what is being removed
## write that down.
apt autoremove
apt update
apt upgrade
apt autoremove
apt dist-upgrade
apt-get install upgrade-system
apt autoremove
apt autopurge

## here too.


## especially here and onward below.
### * This is also the reason why we only run these scripts ONCE
### * On e.g kali, it might be needed to have netcat, ssh, (..)

apt remove telnet* netcat* openssh-server* openssh-client* firefox* deluge* audacious* smplayer* vlc* lxmusic* parcellite*
apt autoremove

apt-get install lxde
apt-get install bash-completion

apt remove telnet* netcat* openssh-server* openssh-client* firefox* deluge* audacious* smplayer* vlc* lxmusic* parcellite*
apt autoremove

apt-get install picom
apt autoremove

echo "reboot now and then MOVE THIS FILE TO   APT_2.DONE.txt"

```

`and reboot`

`*` `mv (apt2 to apt2.done)`






### boot `3#`

#### Pre & Progress Info

```
# 3

date        >> DATE_BOOT_3
timedatectl >> DATE_BOOT_3

uname    >> UNAME_BOOT_3
uname -a >> UNAME_BOOT_3
uname -r >> UNAME_BOOT_3

df --human --all >> DF_BOOT_3
lsblk            >> LSBLK_BOOT_3

```

`* * * * * * * * * * * * * * * * * * * * * * * * * * `
### temp. tools
- these are tools/apps that is used once then removed

`nano tmp_utils.sh`

`* * * * * * * * * * * * * * * * * * * * * * * * * * `

```sh
echo "do not be root, use sudo"
echo "also ONLY RUN THIS ONCE"
echo "[+] temp tools"

echo -e "\e[32m[+] temp tools\e[00m"

sleep 5

## pay attention here to what is being removed
## write that down.
apt autoremove
apt update
apt upgrade
apt autoremove
apt dist-upgrade
apt-get install upgrade-system
apt autoremove
apt autopurge

### #apt remove telnet* netcat* openssh-server* openssh-client* firefox* deluge* audacious* smplayer* vlc* lxmusic* parcellite*
### #apt autoremove

##########
echo -e "\e[31m[+] Installing firefox-esr  MAKE SURE to REMOVE and (. ..) then install firefox from the trusted source. \e[00m"
apt-get install firefox-esr
##########

```

`sudo bash tmp_utils.sh`



### Post Install  

- `sudo apt install gedit xfce4-terminal`

- `optional to do: (from source obviously) bleachbit, cherry tree, joplin`









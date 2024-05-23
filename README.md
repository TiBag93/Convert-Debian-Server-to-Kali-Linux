# Convert-Debian-Server-to-Kali-Linux
Based on  incogbyte/google_cloud_debian_to_kali, but since some parts are outdated I wrote another Script for that

**After you brought a new Server, but unfortunetly they dont offer Kali-Linux, follow the below guide to convert your Debian X to Kali Linux Latest**
I tested this with Debian 9, 10 and 11

# Convert Debian to Kali-Linux:

**Step 1**

`apt update -y && apt full-upgrade -y && apt dist-upgrade -y && apt autoremove -y && apt autoclean`

**Step 2**

`apt install wget gnupg dirmngr`

**Step 3 (Debian > 9)**

`wget https://http.kali.org/pool/main/k/kali-archive-keyring/kali-archive-keyring_2024.1_all.deb`
`dpkg -i kali-archive-keyring_2024.1_all.deb`
`echo "deb http://http.kali.org/kali kali-rolling main non-free contrib" >> /etc/apt/sources.list`

**Step 3 (Debian < 9)**

`wget -q -O - https://archive.kali.org/archive-key.asc | gpg --import`
`echo "deb http://http.kali.org/kali kali-rolling main non-free contrib" >> /etc/apt/sources.list`
`gpg -a --export ED444FF07D8D0BF6 | sudo apt-key add -`

**Step 4**

`apt update -y && apt-get full-upgrade -y && apt-get dist-upgrade -y && apt autoremove -y && apt autoclean`

**Step 5:**

`apt install kali-linux-default`

Other options:

`apt install kali-linux-everything`
`apt install kali-linux-large`
`apt install kali-linux-core`
 

Check the full list of possibilities here:
`https://www.kali.org/tools/kali-meta/`


**Script to update:**

`touch ~/kali_update.sh`

`echo "apt update -y && apt full-upgrade -y && apt dist-upgrade -y && apt autoremove -y && apt autoclean" > ~/kali_update.sh`

`chmod +x ~/kali_update.sh`

**Enable Root Login SSH:**

nano /etc/ssh/sshd_config

PermitRootLogin yes
PasswordAuthentication yes

**Change Keyboard-Layout:

`dpkg-reconfigure keyboard-configuration` 

**Some Tools you might need:**

**Install PIP 3**

`apt install python3-pip`

**Install Bloodhound**

`apt update && sudo apt install -y bloodhound`

**Start Bloodhound**

`neo4j console` Default Credentials: username: neo4j password: neo4j

**Remote GUI:**

Install Gui:

**If you are on GoogleClou** First Create a Firewall Rule for Port 5900 and 5901 in Google Cloud on 0.0.0.0/0

`apt install xfce4 xfce4-goodies -y`

Configure:

`nano ~/.vnc/xstartup`

Put:

#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &

`chmod +x ~/.vnc/xstartup`


First Try with tightvncserver 

`apt install tightvncserver`

Then try with X11vnc if you need.

`apt install x11vnc novnc net-tools`

Set PW:
`x11vnc -storepasswd`

Check:
`ps wwwaux | grep auth`

**Connect with RealVNC**

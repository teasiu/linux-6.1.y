# Pending Deprecation

A few versions ago (around 6.4 IIRC), rtw88x2bu support has been added to the mainline Linux kernel.  This repo will be maintained until we either receive a few comments on https://github.com/cilynx/rtl88x2bu/issues/270 that the mainline driver is working well or [MaxG87](https://github.com/MaxG87) and [cilynx](https://github.com/cilynx) agree that no feedback means no one is still using this driver and we make the executive decision to archive it.

# Driver for rtl88x2bu wifi adaptors

Updated driver for rtl88x2bu wifi adaptors based on Realtek's source distributed with myriad adapters.

Realtek's 5.6.1.6 source was found bundled with the [Cudy WU1200 AC1200 High Gain USB Wi-Fi Adapter](https://amzn.to/351ADVq) and can be downloaded from [Cudy's website](http://www.cudytech.com/wu1200_software_download).

Build confirmed on:

* Linux version `5.4.0-91-generic` on Linux Mint 20.2 (30 November 2021)
* Linux version `5.15.89` on Manjaro (3 February 2023)
* Linux version `5.19` on Ubuntu 22.4
* Linux version `6.1.0-9-amd64` on Debian Bookworm
* Linux version `6.1.*` to `6.12.*` (self-compiled) on Debian and Ubuntu 22.04
* Linux version `6.10.3` to `6.12.10` on Debian Trixie
* Linux version `6.13.0` (self-compiled) on Debian Trixie

As of lately the maintainer experienced issues with the driver on Debian
Testing, covering several Linux Kernel versions. More details can be found in
[issue 280](https://github.com/cilynx/rtl88x2bu/issues/280). Any suggestions on
how to troubleshoot or fix this are welcome there too.

## Using and Installing the Driver

### Simple Usage

In order to make direct use of the driver it should suffice to build the driver
with `make` and to load it with `insmod 88x2bu.ko`. This will allow you
to use the driver directly without changing your system persistently.

It might happen that your system freezes instantaneously. Ensure to not loose
important work by saving and such beforehand.

### DKMS installation

If you want to have the driver available at startup, it will be convenient to
register it in DKMS. This can be done using the script `deploy.sh`, for either

  * all kernels,
  * a specific kernel, or
  * the currently active kernel.

Please consult `--help` for more information and consider reading the script
before executing it.

Since registering a kernel module in DKMS is a major intervention, only execute
it if you understand what the script does.

### Unknown Symbol Errors

Some users reported problems due to `Unknown symbol in module`. A likely cause
of this is that the cfg80211 module is not present in the Kernel. You can fix
this by running it:

    sudo modprobe cfg80211


Another reported cause was that old deployments of the driver were still
present in the system directories. One reported solution was to forcibly remove
all old driver modules. **This is a drastic measure. It may prevent you from
using other external WiFi adapters.** See [this
issue](https://github.com/cilynx/rtl88x2bu/issues/249) for more information.

If you want to proceed anyways, you can run the following commands:

    sudo dkms remove rtl88x2bu/5.8.7.4 --all
    find /lib/modules -name cfg80211.ko -ls
    sudo rm -f /lib/modules/*/updates/net/wireless/cfg80211.ko


### Linux 5.18+ and RTW88 Driver

Starting from Linux 5.18, some distributions have added experimental RTW88 USB
support (include RTW88x2BU support). It is not yet stable but if it works well
on your system, then you no longer need this driver. But if it doesn't work or
is unstable, you need to manually blacklist it because it has a higher loading
priority than this external drivers.

Check the currently loaded module using `lsmod`. If you see `rtw88_core`,
`rtw88_usb`, or any name beginning with `rtw88_` then you are using the RTW88
driver. If you see `88x2bu` then you are using this RTW88x2BU driver.

To blacklist RTW88 8822bu USB driver, run the following command. It will
_replace_ the existing `*.conf` file with the `echo`ed content.

```
echo "blacklist rtw88_8822bu" | sudo tee /etc/modprobe.d/rtw8822bu.conf
```

Then reboot your system.


### Secure Boot

Secure Boot will prevent the module from loading as it isn't signed. In order
to check whether you have secure boot enabled, you couly run  `mokutil
--sb-state`. If you see something like `SecureBoot disabled`, you do not take
to setup module signing.

If Secure Boot is enabled on your machine, you either could disable it in BIOS
or UEFI or you could set up signing the module. How to do so is described
[here](https://github.com/cilynx/rtl88x2bu/issues/210#issuecomment-1166402943).


## Raspberry Pi Access Point

```bash
# Update all packages per normal
sudo apt update
sudo apt upgrade

# Install prereqs
sudo apt install git dnsmasq hostapd bc build-essential dkms raspberrypi-kernel-headers

# Reboot just in case there were any kernel updates
sudo reboot

# Pull down the driver source
git clone https://github.com/cilynx/rtl88x2bu
cd rtl88x2bu/

# Configure for RasPi
sed -i 's/I386_PC = y/I386_PC = n/' Makefile
sed -i 's/ARM_RPI = n/ARM_RPI = y/' Makefile

# DKMS as above
VER=$(sed -n 's/\PACKAGE_VERSION="\(.*\)"/\1/p' dkms.conf)
sudo rsync -rvhP ./ /usr/src/rtl88x2bu-${VER}
sudo dkms add -m rtl88x2bu -v ${VER}
sudo dkms build -m rtl88x2bu -v ${VER} # Takes ~3-minutes on a 3B+
sudo dkms install -m rtl88x2bu -v ${VER}

# Plug in your adapter then confirm your new interface name
ip addr

# Set a static IP for the new interface (adjust if you have a different interface name or preferred IP)
sudo tee -a /etc/dhcpcd.conf <<EOF
interface wlan1
    static ip_address=192.168.4.1/24
    nohook wpa_supplicant
EOF

# Clobber the default dnsmasq config
sudo tee /etc/dnsmasq.conf <<EOF
interface=wlan1
  dhcp-range=192.168.4.100,192.168.4.199,255.255.255.0,24h
EOF

# Configure hostapd
sudo tee /etc/hostapd/hostapd.conf <<EOF
interface=wlan1
driver=nl80211
ssid=pinet
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=CorrectHorseBatteryStaple
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
EOF

sudo sed -i 's|#DAEMON_CONF=""|DAEMON_CONF="/etc/hostapd/hostapd.conf"|' /etc/default/hostapd

# Enable hostapd
sudo systemctl unmask hostapd
sudo systemctl enable hostapd

# Reboot to pick up the config changes
sudo reboot
```

If you want 802.11an speeds 144Mbps you could use this config below:
```
# Configure hostapd
sudo tee /etc/hostapd/hostapd.conf <<EOF
interface=wlx74ee2ae24062
driver=nl80211
ssid=borg

macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=toe54321
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP

hw_mode=a
channel=36
wmm_enabled=1

country_code=US

require_ht=1
ieee80211ac=1
require_vht=1

#This below is supposed to get us 867Mbps and works on rtl8814au doesn't work on this driver yet
#vht_oper_chwidth=1
#vht_oper_centr_freq_seg0_idx=157

ieee80211n=1
ieee80211ac=1
EOF

$ iwconfig
wlx74ee2ae24062  IEEE 802.11an  ESSID:"borg"  Nickname:"<WIFI@REALTEK>"
          Mode:Master  Frequency:5.18 GHz  Access Point: 74:EE:2A:E2:40:62
          Bit Rate:144.4 Mb/s   Sensitivity:0/0
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=0/100  Signal level=-100 dBm  Noise level=0 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```
If you want to setup
[masquerading](https://www.raspberrypi.org/documentation/configuration/wireless/access-point-routed.md)
or
[bridging](https://www.raspberrypi.org/documentation/configuration/wireless/access-point-bridged.md),
check out the official Raspberry Pi docs.

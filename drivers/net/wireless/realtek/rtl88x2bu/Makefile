# SPDX-License-Identifier: GPL-2.0
obj-m := 88x2bu.o

KVERSION := $(shell uname -r)
PWD := $(shell pwd)

# Include subdirectories
subdir-y := core hal os_dep platform hal/rtl8822b hal/halmac hal/phydm hal/led

all:
	$(MAKE) -C /lib/modules/$(KVERSION)/build M=$(PWD) modules

clean:
	$(MAKE) -C /lib/modules/$(KVERSION)/build M=$(PWD) clean

install:
	sudo cp 88x2bu.ko /lib/modules/$(KVERSION)/kernel/drivers/net/wireless/realtek/rtl88x2bu/
	sudo depmod -a

# DKMS support
obj-m := 88x2bu.o
88x2bu-objs := \
	core/rtw_cmd.o \
	core/rtw_io.o \
	core/rtw_security.o \
	core/rtw_xmit.o \
	core/rtw_recv.o \
	core/rtw_pwrctrl.o \
	core/rtw_rf.o \
	core/rtw_mlme.o \
	core/rtw_mi.o \
	core/rtw_ioctl_query.o \
	core/rtw_ioctl_set.o \
	core/rtw_ieee80211.o \
	core/rtw_br_ext.o \
	core/rtw_btcoex.o \
	core/rtw_btcoex_wifionly.o \
	core/rtw_chplan.o \
	core/rtw_sdio.o \
	core/rtw_mp.o \
	core/rtw_ap.o \
	core/rtw_p2p.o \
	core/rtw_tdls.o \
	core/rtw_rm.o \
	core/rtw_rm_fsm.o \
	core/rtw_rm_util.o \
	core/rtw_rson.o \
	core/rtw_wapi.o \
	core/rtw_wapi_sms4.o \
	core/rtw_beamforming.o \
	core/rtw_sreset.o \
	core/rtw_iol.o \
	core/rtw_mem.o \
	core/rtw_wlan_util.o

# Add HAL objects
88x2bu-objs += hal/rtl8822b/rtl8822b_ops.o
88x2bu-objs += hal/rtl8822b/rtl8822b_halinit.o
88x2bu-objs += hal/rtl8822b/rtl8822b_phy.o
88x2bu-objs += hal/rtl8822b/rtl8822b_mac.o
88x2bu-objs += hal/rtl8822b/rtl8822b_cmd.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_ops.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_io.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_recv.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_xmit.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_halinit.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_halmac.o
88x2bu-objs += hal/rtl8822b/usb/rtl8822bu_led.o


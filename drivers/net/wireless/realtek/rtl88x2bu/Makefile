# SPDX-License-Identifier: GPL-2.0
# Makefile for Realtek RTL88x2BU driver
# Always respect kernel Kconfig
obj-$(CONFIG_RTL88X2BU) := 88x2bu.o

# Module objects
88x2bu-objs := \
	core/rtw_cmd.o \
	core/rtw_security.o \
	core/rtw_debug.o \
	core/rtw_mlme.o \
	core/rtw_mlme_ext.o \
	core/rtw_wlan_util.o \
	core/rtw_vht.o \
	core/rtw_pwrctrl.o \
	core/rtw_rf.o \
	core/rtw_recv.o \
	core/rtw_sta_mgt.o \
	core/rtw_ap.o \
	core/rtw_xmit.o \
	core/rtw_p2p.o \
	core/rtw_tdls.o \
	core/rtw_br_ext.o \
	core/rtw_iol.o \
	core/rtw_sreset.o \
	core/efuse/rtw_efuse.o \
	os_dep/osdep_service.o \
	os_dep/linux/os_intfs.o \
	os_dep/linux/usb_intf.o \
	os_dep/linux/usb_ops_linux.o \
	os_dep/linux/ioctl_linux.o \
	hal/hal_intf.o \
	hal/hal_com.o \
	hal/hal_com_phycfg.o \
	hal/hal_com_rtw.o \
	hal/hal_mp.o \
	hal/hal_phy.o \
	hal/hal_dm.o \
	hal/hal_btcoex.o \
	hal/hal_hci/hal_usb.o \
	hal/hal_hci/hal_usb_ops.o \
	hal/rtl8822b/rtl8822b_halinit.o \
	hal/rtl8822b/rtl8822b_phycfg.o \
	hal/rtl8822b/rtl8822b_rf6052.o \
	hal/rtl8822b/rtl8822b_dm.o \
	hal/rtl8822b/rtl8822b_xmit.o \
	hal/rtl8822b/rtl8822b_recv.o \
	hal/rtl8822b/rtl8822b_cmd.o \
	hal/rtl8822b/rtl8822b_led.o \
	hal/rtl8822b/rtl8822b_sreset.o \
	hal/rtl8822b/usb/rtl8822bu_halinit.o \
	hal/rtl8822b/usb/rtl8822bu_halmac.o \
	hal/rtl8822b/usb/rtl8822bu_io.o \
	hal/rtl8822b/usb/rtl8822bu_xmit.o \
	hal/rtl8822b/usb/rtl8822bu_recv.o

# Include standard kernel build rules
obj-m := $(obj-$(CONFIG_RTL88X2BU))


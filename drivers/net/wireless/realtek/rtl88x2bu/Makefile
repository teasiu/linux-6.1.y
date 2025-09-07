# SPDX-License-Identifier: GPL-2.0
# Realtek RTL88x2BU WiFi driver

ccflags-y += $(USER_ccflags-y)
ccflags-y += -O2 -Wall -Wextra
ccflags-y += -Wno-cast-function-type -Wno-type-limits -Wno-unused-function
ccflags-y += -Wno-unused-parameter -Wno-unused-variable -Wno-stringop-overread
ccflags-y += -Wno-array-bounds -Wno-address -Wno-missing-prototypes -Wno-missing-declarations

# 必须加这个，否则 drv_types.h 找不到
ccflags-y += -I$(src)/include

obj-$(CONFIG_RTL88X2BU) := 88x2bu.o

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


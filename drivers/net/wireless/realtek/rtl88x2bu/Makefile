# SPDX-License-Identifier: GPL-2.0
# Makefile for Realtek RTL88x2BU USB wireless driver

obj-$(CONFIG_RTL88X2BU) := 88x2bu.o

88x2bu-objs := \
    core/rtw_cmd.o \
    core/rtw_debug.o \
    core/rtw_io.o \
    core/rtw_ioctl_query.o \
    core/rtw_ioctl_set.o \
    core/rtw_mlme.o \
    core/rtw_mi.o \
    core/rtw_pwrctrl.o \
    core/rtw_rf.o \
    core/rtw_recv.o \
    core/rtw_sta_mgt.o \
    core/rtw_xmit.o \
    core/rtw_ap.o \
    core/rtw_security.o \
    core/rtw_led.o \
    core/rtw_mp.o \
    hal/hal_intf.o \
    hal/hal_com.o \
    hal/hal_cfg.o \
    hal/hal_phy.o \
    hal/rtl8822b/rtl8822b_halinit.o \
    hal/rtl8822b/rtl8822b_mac.o \
    hal/rtl8822b/rtl8822b_phy.o \
    hal/rtl8822b/rtl8822b_recv.o \
    hal/rtl8822b/rtl8822b_xmit.o \
    hal/rtl8822b/usb/rtl8822bu_io.o \
    hal/rtl8822b/usb/rtl8822bu_recv.o \
    hal/rtl8822b/usb/rtl8822bu_xmit.o \
    os_dep/osdep_service.o \
    os_dep/linux/ioctl_linux.o \
    os_dep/linux/os_intfs.o \
    os_dep/linux/usb_intf.o \
    os_dep/linux/usb_ops_linux.o \
    platform/platform_ops.o


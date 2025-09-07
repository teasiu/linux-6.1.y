# Makefile for RTL88x2BU driver

# Module name
obj-m := 88x2bu.o

# Source files for the module
88x2bu-objs := \
	core/rtw_cmd.o \
	core/rtw_debug.o \
	core/rtw_io.o \
	core/rtw_ioctl_query.o \
	core/rtw_ioctl_set.o \
	core/rtw_iol.o \
	core/rtw_mem.o \
	core/rtw_mi.o \
	core/rtw_mlme.o \
	core/rtw_mlme_ext.o \
	core/rtw_pwrctrl.o \
	core/rtw_recv.o \
	core/rtw_rf.o \
	core/rtw_rm.o \
	core/rtw_rm_fsm.o \
	core/rtw_rm_util.o \
	core/rtw_rson.o \
	core/rtw_sdio.o \
	core/rtw_security.o \
	core/rtw_sreset.o \
	core/rtw_sta_mgt.o \
	core/rtw_tdls.o \
	core/rtw_vht.o \
	core/rtw_wapi.o \
	core/rtw_wapi_sms4.o \
	core/rtw_wlan_util.o \
	core/rtw_xmit.o \
	hal/rtl8822b/usb/rtl8822bu_io.o \
	hal/rtl8822b/usb/rtl8822bu_recv.o \
	hal/rtl8822b/usb/rtl8822bu_xmit.o \
	hal/rtl8822b/usb/rtl8822bu_ops.o \
	hal/rtl8822b/usb/rtl8822bu_led.o \
	hal/rtl8822b/usb/rtl8822bu_halinit.o \
	hal/rtl8822b/usb/rtl8822bu_halmac.o

# Kernel build directory
KDIR := /lib/modules/$(shell uname -r)/build

# Extra include paths
EXTRA_CFLAGS := -I$(PWD)/include -I$(PWD)/core -I$(PWD)/hal -I$(PWD)/hal/rtl8822b -I$(PWD)/hal/rtl8822b/usb

# Default target
all:
	$(MAKE) -C $(KDIR) M=$(PWD) modules EXTRA_CFLAGS="$(EXTRA_CFLAGS)"

# Clean
clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean


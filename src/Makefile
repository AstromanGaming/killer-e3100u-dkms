#
#
#

CONFIG_CTAP_SHORT = ON

ifneq ($(KERNELRELEASE),)
	obj-m	 := e3100u.o

	ifneq (,$(filter OFF off, $(CONFIG_CTAP_SHORT)))
		ccflags-y += -DCONFIG_CTAP_SHORT_OFF
	endif

	ifeq (TRUE, $(shell test $(VERSION) -lt 5 && echo "TRUE" || \
		test $(VERSION) -eq 5 && test $(PATCHLEVEL) -lt 12 && echo "TRUE"))
		ccflags-y += -DLINUX_VERSION_MAJOR=$(VERSION)
		ccflags-y += -DLINUX_VERSION_PATCHLEVEL=$(PATCHLEVEL)
		ccflags-y += -DLINUX_VERSION_SUBLEVEL=$(SUBLEVEL)
	endif
else
	KERNELDIR ?= /lib/modules/$(shell uname -r)/build
	PWD :=$(shell pwd)
	TARGET_PATH := kernel/drivers/net/usb
	INBOXDRIVER := $(shell find $(subst build,$(TARGET_PATH),$(KERNELDIR)) -name e3100u.ko.* -type f)
	RULEFILE = 50-usb-killer-net.rules
	RULEDIR = /etc/udev/rules.d/

.PHONY: modules
modules:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules

.PHONY: all
all: clean modules install

.PHONY: clean
clean:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) clean

.PHONY: install
install:
ifneq ($(shell lsmod | grep e3100u),)
	rmmod e3100u
endif
ifneq ($(INBOXDRIVER),)
	rm -f $(INBOXDRIVER)
endif
	$(MAKE) -C $(KERNELDIR) M=$(PWD) INSTALL_MOD_DIR=$(TARGET_PATH) modules_install
	modprobe e3100u

.PHONY: install_rules
install_rules:
	install --group=root --owner=root --mode=0644 $(RULEFILE) $(RULEDIR)

endif


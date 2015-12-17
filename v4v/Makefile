obj-m := v4v.o

KVERSION := $(shell uname -r)
KDIR := /lib/modules/$(KVERSION)/build
PWD := $(shell pwd)

default:
	echo $(MAKE) -C $(KDIR) M=$(PWD) modules -I$(PWD)/include -I$(PWD) EXTRA_CFLAGS="-g -I$(PWD)/include -I$(PWD) -I$(src)"
	$(MAKE) -C $(KDIR) M=$(PWD) modules -I$(PWD)/include -I$(PWD) EXTRA_CFLAGS="-g -I$(PWD)/include -I$(PWD)"

clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean

install:
	$(MAKE) -C $(KDIR) M=$(PWD) modules_install
	install -d ${DESTDIR}/usr/include/xen
	install -m 0644 include/xen/v4v.h ${DESTDIR}/usr/include/xen
	install -d ${DESTDIR}/usr/include/linux
	install -m 0644 linux/v4v_dev.h ${DESTDIR}/usr/include/linux

load:
	-/sbin/rmmod v4v
	/sbin/insmod v4v.ko

PROJ=lora
obj-m := $(PROJ).o

KERNEL_LOCATION=/lib/modules/$(shell uname -r)
BUILDDIR=$(KERNEL_LOCATION)/build

all:
	make -C $(BUILDDIR) M=$(PWD) modules

install:
	gzip $(PROJ).ko
	sudo mv $(PROJ).ko.gz $(KERNEL_LOCATION)/kernel/drivers/spi/$(PROJ).ko.gz
	# Rebuild the kernel module dependencies for modprobe
	sudo depmod -a

uninstall:
	sudo rm $(KERNEL_LOCATION)/kernel/drivers/spi/$(PROJ).ko.gz
	# Rebuild the kernel module dependencies for modprobe
	sudo depmod -a

test:
	make install; echo
	cat /proc/kallsyms | grep $(PROJ); echo
	make uninstall

clean:
	make -C $(BUILDDIR) M=$(PWD) clean

SRC_DIR:=../sys/dev/vale-bpf

vale-bpf-$(VALE_NAME)-objs := $(SRC_DIR)/vale_bpf.o

obj-m:=vale-bpf-$(VALE_NAME).o

LINUX_SRC:=/lib/modules/$(shell uname -r)/build

EXTRA_CFLAGS:= \
	-O3 \
	-DVALE_NAME=\"$(VALE_NAME)\" \
	-DCONFIG_NETMAP \
	-DCONFIG_NETMAP_VALE \
	-std=gnu11 -Wno-declaration-after-statement \
	-I$(CURDIR)/../sys/dev/vale-bpf \
	-I$(CURDIR)/../sys \
	-I$(LINUX_SRC)/include \
	-I$(NSRC) \
	-I$(NSRC)/LINUX \
	-I$(NSRC)/sys \
	-I$(EBPFSRC)/sys \
	-I$(PWD)

EXTRA_SYMBOLS:= \
	$(EBPFSRC)/LINUX/kernel/Module.symvers \
	$(NSRC)/Module.symvers


all:
ifeq ($(VALE_NAME),)
	@echo "Please specify VALE_NAME variable like VALE_NAME=vale0"
else
	make -C $(LINUX_SRC) M=$(CURDIR) CONFIG_NETMAP=m \
		EXTRA_CFLAGS='$(EXTRA_CFLAGS)' KBUILD_EXTRA_SYMBOLS='$(EXTRA_SYMBOLS)' modules
endif

clean:
	make -C $(LINUX_SRC) M=$(CURDIR) clean
	rm -rf $(SRC_DIR)/modules.order $(SRC_DIR)/Module.symvers \
		$(SRC_DIR)/*.o $(SRC_DIR)/*.ko $(SRC_DIR)/.*.o.cmd $(SRC_DIR)/.*.ko.cmd

obj-$(CONFIG_SCSI_QLA_FC) += qla2xxx.o
ifeq ($(KDIR),)
	KDIR ?= /lib/modules/$(shell uname -r)/build
endif

ifeq ($(QUADSTOR_ROOT),)
	QUADSTOR_ROOT := /quadstor/quadstor
endif

ifneq ($(KERNELRELEASE),)
EXTRA_CFLAGS += -I$(QUADSTOR_ROOT)/target-mode/fc/qla2xxx.deb64 -I$(QUADSTOR_ROOT)/export -I$(QUADSTOR_ROOT)/target-mode/fc/common -DLINUX -Werror

obj-m		+= qla2xxx.o

qla2xxx-objs := qla_os.o qla_init.o qla_mbx.o qla_iocb.o qla_isr.o qla_gs.o \
		qla_dbg.o qla_sup.o qla_attr.o qla_mid.o qla_dfs.o qla_target.o \
		qla_sc.o fcbridge.o fcq.o

else
default:
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules
	strip --strip-debug *.ko
endif

clean:
	rm -f *.o *.ko qla2xxx.mod.c .*.*.cmd .*.ko.cmd Module.symvers .*.o.d *.ko.unsigned modules.order
	rm -rf .tmp_versions 

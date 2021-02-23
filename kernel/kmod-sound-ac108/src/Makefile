#
# Peter Yang <turmary@126.com>
# Copyright (c) 2019 Seeed Studio
#
# MIT License
#

uname_r=$(shell uname -r)

# If KERNELRELEASE is defined, we've been invoked from the
# kernel build system and can use its language
ifneq ($(KERNELRELEASE),)
# $(warning KERNELVERSION=$(KERNELVERSION))

#snd-soc-wm8960-objs := wm8960.o
snd-soc-ac108-objs := ac108.o
#snd-soc-seeed-voicecard-objs := seeed-voicecard.o


#obj-m += snd-soc-wm8960.o
obj-m += snd-soc-ac108.o

ifdef DEBUG
ifneq ($(DEBUG),0)
	ccflags-y += -DDEBUG -DAC101_DEBG
endif
endif



else

DEST := /lib/modules/$(uname_r)/kernel

all:
	make -C /lib/modules/$(uname_r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(uname_r)/build M=$(PWD) clean

install:
	sudo cp snd-soc-ac108.ko ${DEST}/sound/soc/codecs/
	sudo depmod -a


.PHONY: all clean install

endif


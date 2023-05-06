# auto-detect subdirs
ifeq ($(CONFIG_ARCH_ATOLL), y)
include $(srctree)/techpack/audio/4.0/config/atollauto.conf
export
endif

# Use USERINCLUDE when you must reference the UAPI directories only.
USERINCLUDE     += \
                -I$(srctree)/techpack/audio/include/uapi \

# Use LINUXINCLUDE when you must reference the include/ directory.
# Needed to be compatible with the O= option
LINUXINCLUDE    += \
                -I$(srctree)/techpack/audio/4.0/include/uapi \
                -I$(srctree)/techpack/audio/4.0/include

ifeq ($(CONFIG_ARCH_ATOLL), y)
LINUXINCLUDE    += \
                -include $(srctree)/techpack/audio/4.0/config/atollautoconf.h
endif

obj-y += 4.0/soc/
obj-y += 4.0/dsp/
obj-y += 4.0/ipc/
obj-y += 4.0/asoc/

# META-SV

Sentinel Value Yocto Layer

## Local.conf

```
MACHINE ??= 'var-som-mx6'
DISTRO ?= 'fslc-xwayland'
PACKAGE_CLASSES ?= 'package_rpm'
EXTRA_IMAGE_FEATURES ?= "debug-tweaks"
USER_CLASSES ?= "buildstats"
PATCHRESOLVE = "noop"
BB_DISKMON_DIRS ??= "\
    STOPTASKS,${TMPDIR},1G,100K \
    STOPTASKS,${DL_DIR},1G,100K \
    STOPTASKS,${SSTATE_DIR},1G,100K \
    STOPTASKS,/tmp,100M,100K \
    HALT,${TMPDIR},100M,1K \
    HALT,${DL_DIR},100M,1K \
    HALT,${SSTATE_DIR},100M,1K \
    HALT,/tmp,10M,1K"
PACKAGECONFIG:append:pn-qemu-system-native = " sdl"
CONF_VERSION = "2"

KERNEL_MODULE_PACKAGE_SUFFIX = "${@legitimize_package_name(d.getVar('KERNEL_VERSION'))}"

IMAGE_INSTALL:append = " curl jq redis tmux sqlite3 libsqlite3-dev mosquitto dropbear lrzsz logrotate libgpiod mtd-utils dnf libdnf cryptodev-module "
DISTRO_FEATURES:append = " wifi "

DL_DIR ?= "${BSPDIR}/downloads/"
ACCEPT_FSL_EULA = "1"
```

had to add `KERNEL_MODULE_PACKAGE_SUFFIX = "${@legitimize_package_name(d.getVar('KERNEL_VERSION'))}"` for some issue with  cryptodev-module that kept happening

# VenomCore assembled tree v2 — spinel

Layout (matches the real MTK build wiring, not a guess this time):

```
kernel-5.10/                              <- Xiaomi_Kernel_OpenSource @ spinel-v-oss
vendor/mediatek/kernel_modules/<name>/     <- each top-level dir from MTK_kernel_modules
kernel_build/                              <- AOSP kernel/build scripts, reference only
```

This mirrors: drivers/misc/mediatek/connectivity/Makefile inside kernel-5.10
expects `$(srctree)/../vendor/mediatek/kernel_modules/connectivity/...` to exist
as a SIBLING directory, and symlinks it in automatically when found — building
WLAN/BT/connfem/etc IN-TREE as part of the normal kernel build, no separate
out-of-tree module build step needed.

Base tag: alps-mp-s0.mp1.tc8sp2-cs1-xm.V1.143.1

Still to verify once you build: whether a defconfig flag like
CONFIG_WLAN_DRV_BUILD_IN=y (or similar) needs to be turned on for the
glue Makefile to actually pick the modules up — check the glue Makefile's
PATH_TO_* / CONFIG_* guards printed by the assembler workflow's log.

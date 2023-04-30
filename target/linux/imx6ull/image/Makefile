#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

#################################################
# Images
#################################################


#################################################
# Devices
#################################################

KERNEL_LOADADDR=0x82000000

define Device/Default
  PROFILES := Generic
  FILESYSTEMS := squashfs ext4
  KERNEL_INSTALL := 1
  KERNEL_SUFFIX := -zImage
  KERNEL_NAME := zImage
  KERNEL_PREFIX := $$(IMAGE_PREFIX)
  KERNEL := kernel-bin none
  IMAGES :=
endef

define Device/alientek
  DEVICE_TITLE := alientek board
  SUPPORTED_DEVICES := alientek pro
  DEVICE_DTS := imx6ull-alientek
  DEVICE_PACKAGES := 
  FILESYSTEMS := squashfs
  IMAGES := combined.bin sysupgrade.bin
  IMAGE_NAME = $$(IMAGE_PREFIX)-$$(1).$$(2)
  IMAGE/combined.bin := append-rootfs
  IMAGE/sysupgrade.bin := sysupgrade-tar | append-metadata
endef
TARGET_DEVICES += alientek

$(eval $(call BuildImage))

#    Copyright (C) 2011 Fundacio Privada per a la Xarxa Oberta, Lliure i Neutral guifi.net
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License along
#    with this program; if not, write to the Free Software Foundation, Inc.,
#    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
#
#    The full GNU General Public License is included in this distribution in
#    the file called "COPYING".
#
# Contributors:
#	Pau Escrich <p4u@dabax.net>
#


include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

QMP_FEED_DIR?=$(CURDIR)

QMP_FEED_DIR?=$(CURDIR)

QMP_GIT_BRANCH?=$(shell git -C $(QMP_FEED_DIR) rev-parse --abbrev-ref HEAD)
QMP_GIT_REV?=$(shell git -C $(QMP_FEED_DIR) rev-parse --short HEAD)
QMP_GIT_DATE?=$(shell git -C $(QMP_FEED_DIR) log -1 --format=%cd --date=format:%Y%m%d)
QMP_GIT_TIME?=$(shell git -C $(QMP_FEED_DIR) log -1 --format=%cd --date=format:%H%M)

QMP_RELEASE?=4.2
QMP_PKGRELEASE=r$(QMP_GIT_DATE)_$(QMP_GIT_TIME)
QMP_CODENAME?=Macondo
QMP_BUILDDATE:=$(shell date +%Y%m%d-%H%M)

PKG_NAME:=bmx6-mdns
PKG_VERSION:=0.1.2-$(QMP_RELEASE)-$(QMP_PKGRELEASE)
PKG_RELEASE:=$(QMP_CODENAME)-$(QMP_GIT_REV)
PKG_LICENSE:=GPL-2.0+

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/bmx6-mdns
  TITLE:=Distributed DNS server based on BMX6 using bmx6-sms plugin
  SECTION:=net
  CATEGORY:=qMp
  URL:=https://qmp.cat
  DEPENDS:=+bmx6-sms
endef

define Package/bmx6-mdns/description
 Distributed DNS system using bmx6 sms plugin
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/bmx6-mdns/install
	$(INSTALL_DIR) $(1)/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/mdns
	$(INSTALL_DIR) $(1)/etc/rc.d
	$(INSTALL_DIR) $(1)/etc/init.d
	$(CP) ./files/etc/init.d/mdns $(1)/etc/init.d/
	chmod 755 $(1)/etc/init.d/mdns
	$(CP) ./files/etc/mdns/* $(1)/etc/mdns
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi/qmp
	$(CP) ./files/luci/bmx6-mdns.lua $(1)/usr/lib/lua/luci/model/cbi/qmp/mdns.lua
endef

$(eval $(call BuildPackage,bmx6-mdns))

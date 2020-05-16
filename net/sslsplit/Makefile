#
# Copyright (C) 2020 Antti Seppälä <a.seppala@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sslsplit
PKG_VERSION:=0.5.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://mirror.roe.ch/rel/sslsplit/
PKG_HASH:=ba0473fd01428439e0cf22fae80fdd26d08a0bcf85e17c82177cb0810b700faf

PKG_MAINTAINER:=Antti Seppälä <a.seppala@gmail.com>
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENCE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/sslsplit
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +libevent2 +libevent2-openssl +libevent2-pthreads +libpcap +libnet-1.2.x +USE_MUSL:musl-fts
  TITLE:=Transparent SSL/TLS interception
  URL:=https://www.roe.ch/SSLsplit
endef

define Package/sslsplit/Default/description
  SSLsplit is a tool for man-in-the-middle attacks against SSL/TLS encrypted
  network connections. It is intended to be useful for network forensics,
  application security analysis and penetration testing.
endef

define Build/Compile
	$(call Build/Compile/Default,PREFIX="/usr" FEATURES="-DHAVE_NETFILTER" PKGCONFIG=$(PKG_CONFIG) LIBNET_BASE=$(STAGING_DIR)/usr $(if $(CONFIG_USE_MUSL),LDFLAGS+=-lfts))
endef

define Build/Install
	$(call Build/Install/Default,PREFIX="/usr" FEATURES="-DHAVE_NETFILTER" PKGCONFIG=$(PKG_CONFIG) LIBNET_BASE=$(STAGING_DIR)/usr $(if $(CONFIG_USE_MUSL),LDFLAGS+=-lfts) install)
endef

define Package/sslsplit/install
	$(INSTALL_DIR) \
	 $(1)/usr/sbin \
	 $(1)/etc/config

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/sslsplit $(1)/usr/sbin/sslsplit
endef

$(eval $(call BuildPackage,sslsplit))

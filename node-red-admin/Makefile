# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=node-red-admin
PKG_NAME:=$(PKG_NPM_NAME)
PKG_VERSION:=0.2.6
PKG_RELEASE:=2

PKG_SOURCE_URL:=https://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_HASH:=69d3ecb54fc7c4a65adf00989fdd8ca540b8ff78269ff81f8ffea140557190ea

PKG_MAINTAINER:=Jan Pavlinec <jan.pavlinec@nic.cz>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=node/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include ../npm-package.mk

define Package/node-red-admin
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Admin tool for node-red
  URL:=https://nodered.org/docs/user-guide/node-red-admin
  DEPENDS:=+node +node-npm
endef

define Package/node-red-admin/description
  The command-line tool allows you to remotely administer a Node-RED instance.
endef

TARGET_CFLAGS+=$(FPIC)
TARGET_CPPFLAGS+=$(FPIC)

define Package/node-red-admin/install
	$(INSTALL_DIR) $(1)/usr/lib/node
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/* $(1)/usr/lib/node/
	$(INSTALL_DIR) $(1)/usr/bin
	$(LN) ../lib/node/$(PKG_NPM_NAME)/node-red-admin.js $(1)/usr/bin/node-red-admin
	$(INSTALL_DIR) $(1)/usr/lib/node_modules
	$(LN) ../node/$(PKG_NPM_NAME) $(1)/usr/lib/node_modules/$(PKG_NPM_NAME)
endef

define Package/node-red-admin/postrm
#!/bin/sh
rm /usr/lib/node_modules/node-red-admin || true
rm -rf /usr/lib/node/node-red-admin || true
endef

$(eval $(call BuildPackage,node-red-admin))

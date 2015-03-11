include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk


RUBY_PKG_LIBVER:=2.2

PKG_NAME:=ruby-eventmachine
PKG_SHORT_NAME:=eventmachine
PKG_RELEASE:=1
PKG_LIBVER:=1.0.7
PKG_REV:=6dbdb97bada05d33a1f0d469a49d8c46ac2e77d0
PKG_VERSION:=$(PKG_LIBVER)

PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_SOURCE_URL:=git://github.com/eventmachine/eventmachine.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git

PKG_BUILD_DEPENDS:=
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/ruby-eventmachine
  SUBMENU:=Ruby
  SECTION:=lang
  CATEGORY:=Languages
  DEPENDS:=+ruby-socket +libstdcpp +libc +libgcc
  TITLE:=Ruby eventmachine gem
endef

RUBY:= \
	$(STAGING_DIR_HOST)/bin/ruby -I $(STAGING_DIR_HOST)/share/ri \


define Package/ruby-eventmachine/description
 This package contains the ruby eventmachine gem.
endef

define Build/Configure/eventmachine
	(cd $(PKG_BUILD_DIR)/ext; \
		$(RUBY) extconf.rb; \
	);
endef

define Build/Compile/eventmachine
	$(MAKE_VARS) \
	$(MAKE) -C $(PKG_BUILD_DIR)/ext \
		$(MAKE_FLAGS) \
		$(1);
	$(CP) $(PKG_BUILD_DIR)/ext/*.so $(PKG_BUILD_DIR)/lib/
endef

define Build/Configure/fastfilereader
	(cd $(PKG_BUILD_DIR)/ext/fastfilereader; \
		$(RUBY) extconf.rb; \
	);
endef

define Build/Compile/fastfilereader
	$(MAKE_VARS) \
	$(MAKE) -C $(PKG_BUILD_DIR)/ext/fastfilereader \
		$(MAKE_FLAGS) \
		$(1);
	$(CP) $(PKG_BUILD_DIR)/ext/fastfilereader/*.so $(PKG_BUILD_DIR)/lib/
endef

define Build/Configure
	$(call Build/Configure/eventmachine)
	$(call Build/Configure/fastfilereader)
endef

define Build/Compile
	$(call Build/Compile/fastfilereader)
	$(call Build/Compile/eventmachine)
endef

define Package/ruby-eventmachine/install
	$(INSTALL_DIR) $(1)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/mips-linux
	$(CP) $(PKG_BUILD_DIR)/lib/eventmachine.rb $(1)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/
	$(CP) $(PKG_BUILD_DIR)/lib/em $(1)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/
	$(CP) $(PKG_BUILD_DIR)/lib/*.so $(1)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/mips-linux
endef

$(eval $(call BuildPackage,ruby-eventmachine))

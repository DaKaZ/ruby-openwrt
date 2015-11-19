include $(TOPDIR)/rules.mk

RUBY_PKG_LIBVER:=2.2
RUBY_PKG_NAME:=ruby
RUBY_PKG_VERSION:=2.2.3

PKG_NAME:=ruby-ffi
PKG_SHORT_NAME:=ffi
PKG_RELEASE:=1
PKG_LIBVER:=1.9.10
PKG_VERSION:=$(PKG_LIBVER)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=git://github.com/ffi/ffi.git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_SHORT_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_MD5SUM=987fb79f7e9256a0493645a7cf14c769

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DEPENDS:=ruby/host
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/ruby-ffi
  SUBMENU:=Ruby
  SECTION:=lang
  CATEGORY:=Languages
  DEPENDS:=ruby +ruby-rbconfig +libffi
  TITLE:=Ruby FFI gem
endef
ifeq ($(ARCH),rlx)
	ARCH:=mips
endif
RUBY:=$(STAGING_DIR_HOST)/bin/ruby --disable=gems \
	-I$(BUILD_DIR)/$(RUBY_PKG_NAME)-$(RUBY_PKG_VERSION) \
	-r$(ARCH)-linux-gnu-fake

define Package/ruby-ffi/description
 This package contains the ruby ffi gem.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR)/ext/ffi_c; \
		$(RUBY) extconf.rb; \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ext/ffi_c
endef

define Build/Install
	$(INSTALL_DIR) $(PKG_INSTALL_DIR)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/$(ARCH)-linux-gnu
	$(CP) $(PKG_BUILD_DIR)/lib/ffi.rb $(PKG_INSTALL_DIR)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/
	$(CP) $(PKG_BUILD_DIR)/lib/ffi $(PKG_INSTALL_DIR)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/
	$(CP) $(PKG_BUILD_DIR)/ext/ffi_c/ffi_c.so $(PKG_INSTALL_DIR)/usr/lib/ruby/$(RUBY_PKG_LIBVER)/$(ARCH)-linux-gnu/
endef

define Package/ruby-ffi/install
	( cd $(PKG_INSTALL_DIR); $(TAR) -cf - \
		usr/lib/ruby/$(RUBY_PKG_LIBVER)/ffi \
		usr/lib/ruby/$(RUBY_PKG_LIBVER)/ffi.rb \
		usr/lib/ruby/$(RUBY_PKG_LIBVER)/*/ffi_c.so \
	) | ( cd $(1); $(TAR) -xf - )
endef

$(eval $(call BuildPackage,ruby-ffi))

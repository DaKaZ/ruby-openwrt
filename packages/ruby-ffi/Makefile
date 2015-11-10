include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk


RUBY_PKG_LIBVER:=2.2

PKG_NAME:=ruby-ffi
PKG_SHORT_NAME:=ffi
PKG_RELEASE:=1
PKG_LIBVER:=1.9.10
PKG_REV:=c60a190d6b05881bdacb8bfda6c88ccea3a2c7e9
PKG_VERSION:=$(PKG_LIBVER)

PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_SOURCE_URL:=git://github.com/ffi/ffi.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_SHORT_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git

PKG_BUILD_DEPENDS:=ruby/host
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/ruby-ffi
  SUBMENU:=Ruby
  SECTION:=lang
  CATEGORY:=Languages
  DEPENDS:=+ruby-socket +libstdcpp +libc +libgcc +libffi
  TITLE:=Ruby FFI gem
endef

RUBY:= \
	$(STAGING_DIR_HOST)/bin/ruby -I $(STAGING_DIR_HOST)/share/ri \


define Package/ruby-ffi/description
 This package contains the ruby ffi gem.
endef

define Build/Configure/ruby-ffi

endef

define Build/Compile/ruby-ffi

endef


define Build/Compile
	$(call Build/Compile/ruby-ffi)
endef

define Package/ruby-ffi/install
	rake gem:install
endef

$(eval $(call BuildPackage,ruby-ffi))

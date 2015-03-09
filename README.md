# Ruby and Ruby Event Machine packages for OpenWrt Barrier Breaker #

Ruby 2.2 Packages cloned from edge package feeds: https://github.com/openwrt/packages  commit:21e433324efc1d5200eef22b61172f13a409a341

Ruby Event Machine inspired by https://github.com/awilliams/ruby-openwrt

## Build Notes ##

If you are compiling / building using OS X, I had to do two things to get everything to build correctly.  First, I was
running ruby 2.2.0 in my host system.  Seconarily, I had to disable ccache, you can do this when you build as such:

`CCACHE_DISABLE=1 make V=s`


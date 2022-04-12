# openwrt-profile
本文主要是维护openwrt的配置文件，包含公司内部dns 主机名的劫持【内部域名解析】的配置文件、dnsmasq的配置文件。

1.内部域名解析的路径/etc/config/dhcp
2.静态路由表路径/etc/config/network  #做旁路由不需要静态路由表，直接去掉带config route 的即可。
3.ssrplus 配置文件路径/etc/ssrplus   #需要注意的是

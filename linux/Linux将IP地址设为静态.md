1. 在 `/etc/sysconfig/network-scripts` 中修改以 `ifcfg-ens` 开头的配置文件，vim 打开
2. 将 BOOTPROTO 从 dhcp 改为 static
3. 添加 IPADDR ，确保 ip 地址与虚拟网卡在同一网段
4. 添加 NETMASK 子网掩码
5. 添加 GATEWAY 网管
6. 添加 DNS
7. 使用 `systemctl restart network` 重启网络
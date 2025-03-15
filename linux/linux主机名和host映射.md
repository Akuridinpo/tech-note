+ `hostname` 指令或者查看 `/etc/hostname` 可以得到主机名
+ 如果想在本机远程 ping 通过名称 ping 通 linux，需要配置 host 文件，让 linux 主机名与 ip 形成映射关系。
+ ping 时的域名解析机制：
  1. 检查浏览器缓存中有没有该域名解析 ip 地址
  2. 检查 DNS 解析器缓存
  3. 检查 hosts 文件映射
  4. 检查公网的DNS 域名服务器
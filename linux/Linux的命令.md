# Linux 关机/重启
+ shutdown 关机
+ shutdown -h now 立即关机
+ shutdown -h 1 分钟后关机
+ shutdown -r 重启
+ halt 关机
+ sync 同步内存数据到硬盘
+ reboot 重启系统
# Linux 用户操作
+ su 用户名称切换用户
+ exit 注销用户
+ whoami 显示当前用户名称
+ who am i 显示当前用户详细信息
+ useradd 用户名创建用户，只有 root 管理员有权限，删除同理
+ useradd -g 组名用户名 将用户创建在选定组下
+ passwd 用户名 给指定用户设定密码
+ userdel 用户名删除用户的数据，但不删除用户目录
+ userdel -r 用户名删除用户的数据和用户目录
+ id 用户名查询用户信息
+ groupadd 组名创建组，同一组的用户的权限相同。
+ groupdel 组名删除组

# Linux 修改运行级别
+ init 数字 将 linux 的运行级别修改
+ 0：关机
+ 1：单用户模式（忘记密码后重置密码）
+ 2：多用户模式但无网络服务
+ 3：多用户状态并有网络服务（无图形化界面，最常用）
+ 4：系统未使用，保留给用户
+ 5：图形化界面
+ 6：系统重启

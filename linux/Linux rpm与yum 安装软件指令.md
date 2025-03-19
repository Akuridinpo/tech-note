# Linux rpm 指令
+ `rpm -q 安装包` 查询 rpm 包
+ `rpm -qi 安装包` 查询详细 rpm 包信息
+ `rpm -ql 安装包` 查询会安装什么文件
+ `rpm -qf 文件` 查询文件属于哪 rpm包
+ `rpm -qa | more` 显示 rpm 列表
	`rpm包` 的格式，以火狐浏览器距离：`firefox-68.10.0-1.el7.centos.x86_64`
	+ firefox: rpm 包名
	+ 68.10.0-1. El 7: 包版本号
	+ centos: linux 操作系统
	+ x86_64:操作系统位数 (`i686` `i386` 是 32 位，norch 是通用)
+ `rpm -e` 删除 rpm 包文件
+ `rpm -e --nodeps` 忽略依赖关系删除
+ `rpm -ivh rpm包全名` 安装程序，i: 安装，v: 详细信息, h: 进度条

# Linux yum 指令
+ `yum` 指令用于自动在网络上下载 rpm 包并安装和配置依赖
+ `yum install` 下载并安装
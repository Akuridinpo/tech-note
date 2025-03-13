# Linux 磁盘分区与文件目录的对应关系
+ 磁盘上的分区需要映射在文件系统的某个目录下，用户访问目录时才可访问对应的磁盘分区，这种映射即称作挂载。
+ 分区挂载的目录成为分区的挂载点。
+ 磁盘分区不可以挂载在同一目录下。
+ 磁盘装入后需要初始化每个分区，获得专属的 UUID 才可挂载在分区下。

# Linux 硬盘类型

|                | 标识   | `x`                                    | ~          |
| -------------- | ---- | -------------------------------------- | ---------- |
| IDE 硬盘()hdx~)  | `hd` | 不同的硬盘类型 ：`a`：基本盘 b：基本从属盘 c：辅助盘 d：辅助从属盘 | 磁盘分区:12345 |
| SCSI 硬盘 (sdx~) | `sd` | 硬盘编号:a: 第一块硬盘 b: 第二块硬盘...              | 磁盘分区:12345 |
使用 `lsblk` 查看磁盘情况：
```
[root@xq101 ~]# lsblk

NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda1      8:0  0 20G 0  part /boot
...
```

# Linux 磁盘挂载实例
1. 使用 `lsblk` 查看新硬盘是否安装成功
```shell
lsblk

NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sdb  8:16    0  1G   0  disk
```
2. 使用 `fdisk /dev/sdb` 为磁盘分区，linux 下硬件也是以文件来描述，硬件描述通常保存在 /dev 目录下，sdb 意思是第二块 scsi 硬盘。
   `fdisk /dev/sdb `
   
   使用 n 指令 `add a new partition`
   
   选择磁盘类型，分区号，扇区起始和扇区结束位置。
   
   使用 w 指令 `write table to disk and exit `

3. 再次使用 `lsblk` 即可检查分区是否成功
```shell
lsblk

sdb 8:16 0 1G 0 disk 
└─sdb1 8:17 0 1023M 0 part
```

4. 使用 `mkfs -t ext4 /dev/sdb1` 为该磁盘分区格式化
5. 此时使用 `lsblk -f` 就能看到新的磁盘分区格式化成功并获得了 UUID
	`└─sdb1 ext4 7338b57e-477b-43c7-a647-1d406234e3c2`
6. 创建个新的目录，作为新磁盘分区的挂载点
```shell
cd /
mkdir newdisk
```
7. 使用 `mount /dev/sdb1 /newdisk` 临时挂载。
8. 再次用 `lsblk -f` 检查挂载是否成功。
   `└─sdb1 ext4 7338b57e-477b-43c7-a647-1d406234e3c2 /newdisk`
9. 此时的挂载是临时挂载，在 linux 重启后就会失效，需要在 `/ect/fstab` 中进行配置。
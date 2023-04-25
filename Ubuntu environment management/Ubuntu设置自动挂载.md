@[toc]

# 图形界面
ubuntu系统提供的Disk可以设置自动挂载
进入Disk选中要设置的分区，点击设置，点击Edit Mount Options，具体设置类似下面讲的命令行
![Edit Mount Options](https://img-blog.csdnimg.cn/4131bc48ce1648ffba6e471c4dac1c39.png#pic_center)下面就是具体的设置，注意要关闭User Session Defaults
![在这里插入图片描述](https://img-blog.csdnimg.cn/60bc2b47c9b5433697447c9a5f047c9d.png#pic_center)


# 命令行
## 挂载
命令lsblk查看所有设备
```bash
$ lsblk
...
sda           8:0    0   1.8T  0 disk 
└─sda1        8:1    0 465.7G  0 part /mnt/063d5374-3910-4b4a-81d4-3efc03e9786e
nvme0n1     259:0    0 465.8G  0 disk 
├─nvme0n1p1 259:1    0  93.2G  0 part /boot/efi
└─nvme0n1p2 259:2    0 186.3G  0 part /var/snap/firefox/common/host-hunspell
```
命令blkid查看设备的信息
```bash
$ lsblk /dev/sda1
/dev/sda1: LABEL="Storage" UUID="063d5374-3910-4b4a-81d4-3efc03e9786e" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="154bf49e-21ba-41b8-b960-e0fcb349481f"
```
命令mount，用于挂载，或者查看当前的挂载信息
```bash
mount
...
/dev/sda1 on /mnt/Storage type ext4 (rw,nosuid,nodev,relatime,x-gvfs-show)
...
```
这表示/dev/sda1挂载在/mnt/Storage
如果我们要设置/dev/sda1自动挂载，就需要修改/etc/fstab文件，这个文件记录了自动挂载的信息
```bash
nano /etc/fstab
```
```bash
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/nvme0n1p2 during installation
...
/dev/disk/by-uuid/063d5374-3910-4b4a-81d4-3efc03e9786e /mnt/Storage auto nosuid,nodev,nofail,x-gvfs-show 0 0
```
这个文件的每一列都代表一条自动挂载的信息
一条自动挂载的信息有这些主要词条
1. 磁盘设备文件名/UUID/LABEL（UUID与LABEL需要注明，如UUID=xxx，LABEL=xxx）
2. 挂载点
3. 磁盘分区的文件系统（该条信息没有，若有则为ext4）
4. 文件系统参数，没有什么要求就设置为default（该信息中为auto nosuid,nodev,nofail,x-gvfs-show)
5. 能否被dump备份（能为1，不能则为0）
6. 是否以fsck检验扇区（是为1，否为0）


下面这一节可以跳过
## 文件属性
default：async，auto，rw，exec，nouser，suid等
在挂载信息中没有注明时，使用default中的参数
1.async/sync，异步/同步读写
2.auto/noauto，使用命令mount -a时是否主动测试挂载
3.rw/ro，可读写/只读
4.exec/noexec，可执行/不可执行，限制在文件系统内是否可以进行【命令执行】工作
5.user/nouser，是否允许一般user使用mount命令挂载该系统
6.suid/nosuid，允许SUID/不允许，如果不存放执行文件，可以使用nosuid来限制

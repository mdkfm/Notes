# 在Ubuntu系统中创建桌面快捷方式
## 一般创建方法
在目录/usr/share/applications下，有安装软件时自动生成的的桌面快捷方式，将其复制到你的桌面
修改权限，右键图标，点击allow lauching后快捷方式即可使用

##  自定义创建方法
在你的桌面文件夹新建一个文本文件，举例说明
> [Desktop Entry]
Encoding=UTF-8
Name=JetBrains Toolbox
Comment=JetBrains Toolbox
Exec=/home/skf/.local/share/JetBrains/Toolbox/bin/jetbrains-toolbox
Icon=/home/skf/.local/share/JetBrains/Toolbox/toolbox.svg
Terminal=false # open software is run  Terminal
Type=Application
Categories=Application;Development;

第一行的[Desktop Entry]标志这是一个桌面快捷方式。
Encoding是编码，Name是程序名，Comment为额外说明。
Exec是二进制程序执行的绝对路径，Icon是桌面图标文件绝对路径。
Terminal是否开启一个终端执行，Type是快捷方式类型，Categoties是分类标识。

然后和一般创建方法一样，修改权限，allow lauching。

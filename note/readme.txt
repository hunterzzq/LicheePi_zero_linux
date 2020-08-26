1.得到zImage与dtb
kk用的是https://github.com/hunterzzq/LicheePi_zero_linux.git(来源于git clone https://github.com/Lichee-Pi/linux.git -b zero-4.14.y)
    
1).编译kernel
    生成荔枝派Zero 默认配置文件： make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- licheepi_zero_defconfig
    编译内核: make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
    获得：linux-zero-4.14.y/arch/arm/boot/zImage 



2).设备树, Linux
    编译设备树： make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- dtbs
    获得设备树：arch/arm/boot/dts/sun8i-v3s-licheepi-zero-dock.dtb


2.开机图片：这里kk用的是800x480像素的图片
drivers/video/logo/logo_linux_clut224.ppm是默认的启动Logo图片,把自己的Logo图片(png格式)转换成ppm格式,替换这个文件

GIMP(其他发行版自己安装就行了)。
1).将颜色数改为224(在GIMP中一次选择 图像->模式->索引。）
2).另存为,保存为ppm格式,在弹出的对话框中选择Ascii,然后复制到Logo文件夹替换原来的文件,同时删除
logo_linux_clut224.c	logo_linux_clut224.o文件

3.隐藏启动光标
在内核的当前目录进入到drivers/video/console/fbcon.c文件
将static void fb_flashcursor(void *private),static void	fbcon_cursor(struct vc_data *vc, int mode)用空函数替换。

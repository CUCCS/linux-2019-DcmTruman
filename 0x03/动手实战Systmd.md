# 动手实战Systmd


systemd好强大啊，体验一圈下来感觉以前用的那些配置指令好多都过时了

asciinema上传的时候，出现`pip broken`的错误，怀疑是录制文件过大超出了限制，分段录制之后没有这个问题

## 教程录像

### 第1-3节

[![asciicast](https://asciinema.org/a/nBF24bmBIgkMeBRx4kS7l2k40.svg)](https://asciinema.org/a/nBF24bmBIgkMeBRx4kS7l2k40)

### 第4节

[![asciicast](https://asciinema.org/a/v9SOvRYO4U269vwG0TWavseeI.svg)](https://asciinema.org/a/v9SOvRYO4U269vwG0TWavseeI)

### 第5节

[![asciicast](https://asciinema.org/a/RFT9Eist31nJ4yj1GK8dcOLGs.svg)](https://asciinema.org/a/RFT9Eist31nJ4yj1GK8dcOLGs)

### 第6节

[![asciicast](https://asciinema.org/a/rOPJwfJqHF6r03G0IThE8mC7R.svg)](https://asciinema.org/a/rOPJwfJqHF6r03G0IThE8mC7R)

### 第7节

[![asciicast](https://asciinema.org/a/zQ4bCBEUbIfS91GHtMsvigKrv.svg)](https://asciinema.org/a/zQ4bCBEUbIfS91GHtMsvigKrv)


## 自查清单

1. 如何添加一个用户并使其具备sudo执行程序的权限？
	- 通过`adduser username`添加用户
	- 将`username`放到`sudo`用户组即可获得

2. 如何将一个用户添加到一个用户组
	- `sudo adduser username sudo`

3. 如何查看当前系统的分区表和文件系统详细信息
	- 通过`sudo sfdisk -l`或`sudo cfdisk`查看分区表
	- 通过`df -a`或`stat -f`查看文件系统详细信息

4. 如何实现开机自动挂载Virtualbox的共享目录分区
	- 首先在vbox中打开添加共享文件夹,打开自动挂载和固定分配
	- `sudo /media/cdrom/./VBoxLinuxAdditions.run`安装增强功能
	- `sudo mount -t vboxsf shared ~/shared`将共享文件夹挂载到share目录
	- virtualbox中的选项**自动挂载**可以实现开机自动挂载，也可以通过systemd实现
	- 编写文件`my_mount-src_host.automount`
	
	```bash
	[Unit]
	Description=Auto mount shared "src" folder
	
	[Automount]
	Where=~/shared
	DirectoryMode=0775
	Type=vboxsf
	
	[Install]
	WantedBy=multi-user.target

	```
	- 执行`systemd enable my_mount-src_host.automount`

5. 基于LVM（逻辑分卷管理）的分区如何实现动态扩容和缩减容量？

	```bash
	#缩容
	lvreduce --size size dir
	#扩容
	lvextend --size size dir
	```
	
6. 如何通过systemd设置实现在网络连通时运行一个指定脚本，在网络断开时运行另一个脚本？
	- 网络连通启动脚本配置

	
	```bash
	[Unit]
	Description=After network up
	After=network.target network-online.target 	
	[Service]
	Type=oneshot
	ExecStart=_YOUR_SCRIPT_
	
	[Install]
	WantedBy=multi-user.target

	```
	
	- 网络断开启动脚本配置，我是将上述文件中的`After`改成`Before`

7. 如何通过systemd设置实现一个脚本在任何情况下被杀死之后会立即重新启动？实现杀不死？
	- 创建service文件
	
		```bash
		[Unit]
		Description=My Script
		
		[Service]
		Type=forking
		ExecStart=/usr/bin/MY_SCRIPT
		ExecStop=/usr/bin/MY_SCRIPT
		Restart=always
		RestartSec=1
		RemainAfterExit=yes
		
		[Install]
		WantedBy=multi-user.target
		```
	- 重新加载配置,并启动，其中在MY_SCRIPT中添加一句`systemd start my_script.service`,再次避免services被停止

	



![](https://i.postimg.cc/g0f2X0Dv/ParrotOS.png)

> 安装依赖和lua

* **安装依赖**

  `sudo apt install libreadline-dev -y`

* **这个小功能基于lua，所以先安装lua**

* **[官网](https://www.lua.org/download.html)下载并解压lua压缩包**

  `wget https://www.lua.org/ftp/lua-x.x.x.tar.gz && tar -zxvf lua-x.x.x.tar.gz`

* **进入lua文件夹，测试，编译，安装**
  ```
  cd lua-x.x.x

  sudo make linux test && sudo make linux && sudo make install
  ```

* *Parrot3.5以上的版本不支持apt install安装parrot-conky*

> 【方案一、】安装conky-all

* `sudo apt install conky-all -y`

* **克隆本项目，按相应位置移动**
  ```
  #  备份原有conf配置文件
  sudo mv /etc/conky/conky.conf /etc/conky/conky.conf.bak

  sudo mv ./etc/conky/*  /etc/conky/

  sudo mv ./etc/skel/.config/autostart/* /etc/skel/.config/autostart/

  mv ./root/.config/autostart/conky-start.desktop /home/$(whoami)/.config/autostart

  sudo mv ./usr/share/applications/conky-start.desktop /usr/share/applications/

  sudo mv ./usr/share/fonts/truetype/future/ /usr/share/fonts/truetype/

  # 可以选择把applications里面的图标拷贝到桌面
  cp /usr/share/applications/conky-start.desktop ~/Desktop
  ```
> 【方案二、】官方的一些步骤

* *git clone 库之后*

* **[官方Parrot-Conky_v2.0](https://dev.parrotsec.org/parrot/parrot-conky)给出的建议是安装conky-manager**

  `sudo apt install conky-manager -y`

* **之后启动conky-manager**

* **里面会有一个默认给的主题，如果想用的话，直接点Themes，然后在主题前面打√，就会启用**

* *如何启用Parrot-conky*

  **点击右上角类似控制器的按钮，然后点Locations，再点add，选择你克隆的conky库里面的conky文件夹**

  **然后重启conky-manager，你会发现在Widgets里面有个conky.config的文件，直接打√就会启用(此时启用是没有任何有用的效果的)**

  *所以需要把库里的parrot.png和rings.lua复制到/etc/conky*

  ```
  sudo cp -r ./etc/conky/*  /etc/conky/

  sudo mv ./usr/share/fonts/truetype/future/ /usr/share/fonts/truetype/
  ```

* **设置开机自启**

  *点击General，开启即可*

  ![](https://i.postimg.cc/FsZ3YQTP/20181025193403.png)

* **conky-manager可以安装一些主题包，不过需要各位去下载了，目前我没有收集**

* *弊端：*

* *每次你想改lua主题和config配置文件的时候，你需要在两个文件夹来回切换着改… …*

> Conky新语法

* `sudo ln -sf /usr/local/bin/lua /usr/bin/lua`

* `sudo chmod +x /usr/share/doc/conky-all/convert.lua`

* `/usr/share/doc/conky-all/convert.lua conky.conf`

> 存在问题

* *解决非sudo启动conky不显示发行版本号和/home的磁盘使用情况 --> 就是使用sudo啦*

  `sudo conky`

* *目前新配置文件修改了parrot-conky的大小，以及lua脚本的一些参数，可能存在些许问题*

* *如需切换之前配置文件，请自行查找之前提交的commits*

* *目前修改的lua样式文件只支持4核，如果你的物理机或者虚拟机达不到4核，你就需要去修改lua文件，把一些带有cpu参数的配置删掉，或者屏蔽*

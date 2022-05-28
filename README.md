# __`opencv`及`opencv_contrib`下载__
- [opencv下载地址](https://opencv.org/releases/)  
> 进入后选择你所需要的`opencv`版本点击`Sources`版本下载  
> 下载后为`zip`压缩包格式  
- [opencv_contrib下载地址](https://github.com/opencv/opencv_contrib)  
> 进入后点击`Tags`，之后选择与你下载`opencv`相同版本进行下载  
## __opencv环境配置__    
- __环境配置__  
> 编译环境及支持包
```shell
sudo apt-get install build-essential 
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```  
> __安装`pip`__  
```shell  
sudo apt-get install python-pip python3-pip
```  
> __安装`numpy`和`matplotlib`__  
```shell
sudo pip3 install numpy matplotlib
```  
> __`libjasper`无法找到路径解决方案__  
```shell
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"  
sudo apt install libjasper1 libjasper-dev  
```  
- __编译`opencv`__  
> 进入opencv文件夹创建`build`文件夹，之后进行`cmake`，具体代码如下  
```shell
mkdir build
cd build
sudo cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..  
sudo make  
sudo make install  
```  
> `opencv_contrib`是`opencv`的附加视觉代码库，具有许多`opencv`没有的强大功能，如人脸识别等模块  
> 首先先将`opencv_contrib`放入`opencv`文件夹中，好方便后续编译  
> 随后再次进入`opencv`的`build`文件夹，再次`cmake`  
```shell
sudo cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../opencv/opencv_contrib/modules -D ENABLE_CXX11=1 ..  
其中/opencv前的..为你的opencv路径  
sudo make  
sudo make install  
```  
> 你也可以选择多线程编译，不过并不建议使用，多线程编译可能会出现莫名其妙的错误  
> 下面为多线程编译命令  
```shell
sudo make -j8  
//-j后的数字为线程数  
```  
> `make`80%左右可能会提醒你`src`中找不到`boostdesc`等文件，你可以在上面文件中下载`boostdesc_pkg`，解压后将内置文件全部复制如`error`文件夹内  
> 继续`make`到90%左右会提醒你一系列文件无法找到，是将`opencv_contrib`内置于`opencv`文件夹中的原因  
> 只需到`error`文件对应位置将对应文件地址改为绝对地址即可  
- __配置`opencv`路径__  
```shell
sudo gedit /etc/ld.so.conf.d/opencv.conf  
```  
> 进入文件内后加入下述内容  
```shell
/etc/local/lib
```  
> 之后保存退出(先按`Esc`，后输入 `:wq`)  
> 之后在终端输入下述命令使其保存生效  
```shell
sudo ldconfig
```  
> 随后创建并编辑`bash`文件  
```shell
sudo gedit /etc/bashrc
```  
> 在末尾加入下列命令  
```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig  
export PKG_CONFIG_PATH  
```  
> 保存退出，然后`source`  
```shell
source /etc/bash.bashrc  
```  
- __环境检查__ 
> 在终端输入以下命令  
```shell
sudo apt-get install mlocate  
sudo apt-get updatedb  
sudo gedit /etc/profile  
```  
> 在文件结尾添加：  
```
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH  
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib  
```  
> 保存退出后输入命令  
```shell
pkg-config opencv --modversion  
```  
> 如果终端输出了你所安装的`opencv`版本  
> 恭喜你成功了  
### __Other__  
> 下面为`opencv`所需的全部支持文件，可以根据情况选择是否添加  
```shell
$ sudo apt-get install build-essential cmake git unzip pkg-config zlib1g-dev
$ sudo apt-get install libjpeg-dev libjpeg8-dev libjpeg-turbo8-dev
$ sudo apt-get install libpng-dev libtiff-dev libglew-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
$ sudo apt-get install libgtk2.0-dev libgtk-3-dev libcanberra-gtk-dev
$ sudo apt-get install python-all-dev python-setuptools python-wheel
$ sudo apt-get install python3-dev python3-numpy python3-pip
$ sudo apt-get install libxvidcore-dev libx264-dev libgtk-3-dev
$ sudo apt-get install libtbb2 libtbb-dev libdc1394-22-dev libxine2-dev
$ sudo apt-get install gstreamer1.0-tools libgstreamer-plugins-base1.0-dev
$ sudo apt-get install libgstreamer-plugins-good1.0-dev
$ sudo apt-get install libqt5core5a libqt5gui5 libqt5opengl5 libqt5widgets5 
$ sudo apt-get install libv4l-dev v4l-utils qv4l2
$ sudo apt-get install libtesseract-dev libxine2-dev libpostproc-dev
$ sudo apt-get install libavresample-dev libvorbis-dev
$ sudo apt-get install libfaac-dev libmp3lame-dev libtheora-dev
$ sudo apt-get install libopencore-amrnb-dev libopencore-amrwb-dev
$ sudo apt-get install libopenblas-dev libatlas-base-dev libblas-dev
$ sudo apt-get install liblapack-dev liblapacke-dev libeigen3-dev gfortran
$ sudo apt-get install libhdf5-dev libprotobuf-dev protobuf-compiler
$ sudo apt-get install libgoogle-glog-dev libgflags-dev
$ sudo apt-get install libgphoto2-dev  
```  
> __`python`书写opencv__  
  
> 在终端输入命令  
```shell
sudo gedit ~/.bashrc  
```  
> 在文件末尾加入  
```
export PATH=/home/../.local/bin/:$PATH  
//`..`为你系统用户名  
```  
> 保存退出后`source`  
```shell
source ~/.bashrc  
```  
  
> 安装`opencv`对`python`的接口  
```shell
pip3 install opencv-python  
pip3 install opencv-contrib-python  
```  
  
> 验证接口安装是否正确  
> 进入`python`解释器  
```shell
python3  
```  
> 输入  
```python
import cv2
print(cv2.__version__)  
# 注意是两个`_`  
```  
> 输出你的`opencv`版本即安装成功  
- __环境污染问题解决__  
> 在解决`libjasper`安装时添加了`ppa`，可用下述命令进行`ppa`的清理  
```shell
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"  
```   

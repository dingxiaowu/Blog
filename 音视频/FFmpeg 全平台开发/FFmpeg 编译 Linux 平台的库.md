### 命令安装

```shell
1.升级yum
#  sudo yum install epel-release -y
#  sudo yum update -y

2.安装Nux Dextop Yum 源
#  sudo rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
#  sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm

3.安装FFmpeg 和 FFmpeg开发包
#  sudo yum install ffmpeg ffmpeg-devel -y

4.测试
#  ffmpeg


比较新的
yum install yum-utils
yum install epel-release
yum install https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm
yum update
yum install ffmpeg ffmpeg-devel

//后面关闭自动更新
yum-config-manager --disable epel rpmfusion-free-updates
yum update

centos 7 安装ffmpeg4最新版
yum-config-manager --add-repo=https://negativo17.org/repos/epel-multimedia.repo
yum-config-manager --disable epel-multimedia
yum install --enablerepo=epel-multimedia ffmpeg ffmpeg-devel

File “/bin/yum-config-manager“, line 135 except yum.Errors.RepoError, e:
到指定文件添加2.7版本的注明,使用旧版本
vi /usr/bin/yum-config-manager
```

Centos 安装最新版本 ffmpeg

```
https://www.4dmayi.com/3064.html
https://www.4dmayi.com/3064.html
```

centos 源码编译 ffmpeg

https://www.jianshu.com/p/94a1759ceb34





###源码编译安装

```shell
#!/usr/bin/env bash
# 源码编译ffmpeg动态库
# 需要root权限
# 本脚本的最新版本请访问  https://pengrl.com/p/20029/

set -x

# 编译yasm，ffmpeg依赖的汇编优化的库
wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
tar xvf yasm-1.3.0.tar.gz
cd yasm-1.3.0/
./configure
make
make install
cd -

# 编译nasm依赖的汇编优化的库
wget https://www.nasm.us/pub/nasm/releasebuilds/2.14.02/nasm-2.14.02.tar.gz
tar xvf nasm-2.14.02.tar.gz
cd nasm-2.14.02/
./configure
make
make install
cd -

# 编译x264
wget https://code.videolan.org/videolan/x264/-/archive/master/x264-master.tar.bz2
tar xvf x264-master.tar.bz2
cd x264-master/

./configure --enable-static --enable-shared --disable-asm --disable-avs

make &&  make install
cd -

#编译x265
#编译fdk-aac
#编译mp3



# 编译ffmpeg
#wget https://ffmpeg.org/releases/ffmpeg-4.3.2.tar.bz2
#tar -zxvf ffmpeg-4.3.2.tar.bz2
cd ffmpeg-4.3.2
FFMPEG_PREFIX=/home/DevYK/package/ffmpeg/n4.3.2

./configure \
--prefix=$FFMPEG_PREFIX \
--enable-nonfree \
--enable-shared \
--enable-pthreads  \
--enable-version3  \
--enable-avresample  \
--enable-ffplay   \
--enable-gpl  \
--enable-libmp3lame   \
--enable-libx264   \
--enable-libx265   \
--enable-libfdk-aac \
--disable-optimizations \
--enable-pthreads \
--enable-nonfree \
--enable-libtheora \
--enable-libvorbis \
--enable-libvpx \
--enable-libxvid \


make -j8
make install
./ffmpeg
```








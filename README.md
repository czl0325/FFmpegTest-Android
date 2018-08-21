# FFmpegTest-Android
ffmpeg在android系统的编译导入以及开发


## 下载ffmpeg库

下载地址： http://ffmpeg.org/    点击download，我这边下载的是 4.0.2版本。

## 编译ffmpeg库 

把下载库解压后拷贝到ubuntu系统中，我放在桌面上

```
 $ sudo apt-get install yasm    

 $ ./configure --enable-shared --prefix=/home/work/soft/ffmpeg/

 $ make   #漫长的等待

 $ sudo make install 
```

#### 问题

编译出来会发现so文件是.so.56   如libavformat.so.58 这个在安卓里面是识别不到的，必须把.so放在最后面，这时候就要修改configure文件了。

找到这四行，注释掉

```
#SLIBNAME_WITH_MAJOR='$(SLIBNAME).$(LIBMAJOR)'
#LIB_INSTALL_EXTRA_CMD='$$(RANLIB) "$(LIBDIR)/$(LIBNAME)"'
#SLIB_INSTALL_NAME='$(SLIBNAME_WITH_VERSION)'
#SLIB_INSTALL_LINKS='$(SLIBNAME_WITH_MAJOR) $(SLIBNAME)'
```

改成

```
SLIBNAME_WITH_MAJOR='$(SLIBPREF)$(FULLNAME)-$(LIBMAJOR)$(SLIBSUF)'
LIB_INSTALL_EXTRA_CMD='$$(RANLIB)"$(LIBDIR)/$(LIBNAME)"'
SLIB_INSTALL_NAME='$(SLIBNAME_WITH_MAJOR)'
SLIB_INSTALL_LINKS='$(SLIBNAME)'
```

这样打包就没有问题了

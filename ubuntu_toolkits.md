记录使用ubuntu过程中出现问题的一些解决方法

## 一、ubuntu常用软件列表
1. 中文输入法：搜狗输入法,[配置方法](https://shurufa.sogou.com/linux/guide)
2. 相册自托管：[immich](https://github.com/immich-app/immich)Immich 是一个直接从 iPhone、Android 手机上备份照片与视频的开源解决方案，通过部署在自己的电脑、NAS、服务器中，使用 App 进行备份。界面酷似 Google Photos，支持多用户、照片和相册分享、好友上传、地理位置、机器学习识别事件等功能。是居家备份照片的好帮手。




## 二、常见问题解决方法
### 1. ubuntu 搜狗输入法重启方法
1. 查看fcitx的pid
```shell
pidof fcitx
kill PID #该PID指的是查找的PID
```

2. 重启fcitx
`fcitx
`
### 2. 在Linux（Ubuntu）下安装Arial、Times New Roman等字体
在Linux下做文档、作图的时候，可能需要用到Arial和Times New Roman等字体。但是由于版权问题，Linux一般是不直接提供这些字体的。

以Ubuntu为例，执行以下指令即可：

```shell
sudo apt install ttf-mscorefonts-installer # 安装
sudo fc-cache # 生效
```
由于前面提到版权问题，虽然这部分字体不收费，但是安装时需要用户同意一些协议，同意即可。

执行完成后，用以下指令确认成功：
```shell
fc-match Arial # 查看Arial
fc-match Times # 查看Times New Roman
```
安装完字体后，这些软件需要重启才能看到新安装的字体。
[参考链接](https://www.cnblogs.com/xia-weiwen/p/10336896.html)

## 三、开发工具
1. tee：将标准输出重定向到文件，同时显示在屏幕上

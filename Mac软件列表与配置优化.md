# **我的Mac软件列表**

## 必备应用

1. Google Chrome -最快的浏览器
2. Safari-苹果自带
3. Obsidian - 私密且灵活的笔记应用程序
4. Picview - 轻量图片浏览器

## 效率

1. uTools - 一款基于插件的程序员效率工具，包含非常多的实用插件，如图床、UUID、密码、翻译、JSON格式化等
2. PixPin - 屏幕截图，录制屏幕，长截图，文字识别，贴图，以及更多功能
3. Pot App - 跨平台划词翻译和OCR 💰
4. Bob - 划词翻译和OCR 💰
5. FastZip - 解压缩软件
6. Input Source Pro - 自动切换输入法 💰
7. Dropover - macOS文件拖放增强工具 💰
8. KeyCue - 快捷键辅助工具 💰
9. LocalSend - 跨平台的文件传输工具，界面简洁

## 开发
### 软件工具

1. JetBrains Toolbox App - 管理已安装的JetBrains工具，下载新工具并打开最近的项目。💰

2. CLion - 强大的 C 和 C++ IDE。(学生免费)
3. AppCode - 适用于 iOS / macOS 开发的智能 IDE
4. PyCharm - 一款 Python 开发集成环境，有专业版和社区版。
5. VS Code - 微软推出的免费/开源编辑器，TypeScript 支持杠杠的
6. Vim - Vim 古老的终端中使用的编辑器
7. XTermainal - SSH 工具，功能丰富很好用

### 虚拟机
1. OrbStack - 在 Mac 上无缝高效地运行 Docker 和 Linux。Docker Desktop 替代品，可帮助您更快地工作。

2. Parallels Desktop - Mac 最推荐的虚拟机软件，支持Windows融合💰
3. VMware Fusion Pro - 行业标准桌面虚拟机软件，个人免费使用

## 生产力

1. Microsoft Office - 微软Office办公套件 💰
2. WPS - 是一套跨平台的办公室软件套件。
3. Adobe Photoshop - 顶尖图像编辑与设计软件💰
4. 剪映 - 全能易用的桌面端剪辑软件

## 作图工具

1. Draw.io - 上百种图形，支持多种格式导出。
2. ProcessOn - 流程图、思维导图、原型图... 中文友好，免费保存 5 个文件💰

## 通信

1. QQ - QQ for Mac App
2. 微信 - 微信 for Mac App
3. 腾讯会议
4. Outlook - 微软邮箱管理

## 娱乐

1. QQ音乐

2. IINA-优雅万能视频音频播放器
3. VidHub- 强大的本地与网络视频播放器

## 网盘

1. 百度云盘

2. 阿里云盘
3. 夸克网盘 - 最近推广比较猛的，新资源都在夸克网盘
4. 迅雷下载
5. 123网盘
6. 坚果云网盘

## 系统


1. CleanMyMac - 首款全功能的MacBook 清理工具 💰
2. Ice - 开源的菜单栏整理
3. 超级右键 - 一款finder右键菜单扩展，包括了大量便捷工具比如新建文件，直接打开终端等
4. Appcleaner- 应用卸载工具
5. Stats - 这是迄今为止最详细的 Mac 性能监视器。
6. SoundSource - 应用音频单独控制工具
7. Supercharge - 系统增强工具(剪切文件快捷键、Dock点击图标最小化)
8. Applite - 用户友好的 Homebrew Casks GUI macOS 应用程序

## 命令行工具


1. autojump - 告别又臭又长的路径名，一键直达任何目录。
2. Homebrew - 体验通过命令行安装 Mac 软件的工具(大部分是命令行工具)
3. Zsh - 一个专为交互式使用而设计的命令行 shell。
4. ohmyzsh - 一个由社区驱动,用于管理zsh配置的命令行工具。

## 其他
1. Bitwarden - 强大的开源密码管理器
2. Input-leap - 开源的跨平台KVM切换软件，共享鼠标好键盘









# Mac配置优化

## 隐藏Dock，加速响应

默认情况下，Dock 自动隐藏后会有一点延迟，影响效率。你可以去掉这个延迟，让它秒回：

```
defaults write com.apple.dock autohide-delay -float 0; killall Dock
```

如果想让 Dock 弹出速度更快，加上这个命令：

```
defaults write com.apple.dock autohide-time-modifier -float 0.1; killall Dock
```

想恢复默认用这个：

```
defaults delete com.apple.dock autohide-delay
defaults delete com.apple.dock autohide-time-modifier
killall Dock
```

## Mac + VMware 安装 Ubuntu 虚拟机

1. 软件/镜像下载 VMware-Fusion-13.6.2: [https://pan.quark.cn/s/0e6f0cbc8e44](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa1VCQjNYcXJfWlJUb1gydVJQSS1kR0tXeklIZ3xBQ3Jtc0tsakR1eFduNzJxOWQwYmE3d0ZEcHFpeEVacWMzNENVdUhPMVpueUc2bjFrdjdsWE10RFo4WkhtMk1BbjNqS1QwNzRlb0tZaW9DRG9IRnFnclZtemNQOGJFZURybGdxbUFKd2lzZmRGbG1Qckkxam9WUQ&q=https%3A%2F%2Fpan.quark.cn%2Fs%2F0e6f0cbc8e44&v=vaCZgu7S2CE) VMware-Fusion-13.6.1: [https://pan.quark.cn/s/dd6e1a82a561](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbG5yclpzeGdnT05zSTNPQmJBY1llZzJxd2dhQXxBQ3Jtc0tsMHNrb2trUGtoUVFGcWpxZER0TXJuRmRhZzk0WlZRQTF3R1pGbmEwbW90RGRYenJWVkI0a1RKZ3NOaEhIc2RNdHY4a2pXeW9Na2h3OEROMnRqVzA4TzRiLUFOejVaY1pRUE03RnNqMm1ZNGw4dlY4Zw&q=https%3A%2F%2Fpan.quark.cn%2Fs%2Fdd6e1a82a561&v=vaCZgu7S2CE) VMware-Fusion-13.6.0: [https://pan.quark.cn/s/418ff918c58a](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbjEwdnhOYUVPYUpJdDRsUGw1djJkRUx4SVJid3xBQ3Jtc0trZnpIbkFmaUpldHNIUVZSb0NiSGtOZUwzcVZYVTdIVlIwMjZxS0pmWlJlVm85MnR3NVNVamNFNU05T3dCYTExRWEtRU5tSHhid1NEeEZEZVMxOERtYVpQb2dMQ2gxaFBXcXpiM09RQVc5dXY0WVVESQ&q=https%3A%2F%2Fpan.quark.cn%2Fs%2F418ff918c58a&v=vaCZgu7S2CE) VMware-Fusion-13.5.2: [https://pan.quark.cn/s/39bb114e3214](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbk5ucEJ3RG9ZSFIzQ1Q2bk0yVVJabWtvQXB5QXxBQ3Jtc0ttY3pPaC1QMHRPQTFITDRzSUlnX1BxLXZuTWh2ZXdRYnBYMk5hTm9ESEtYT2d4UDhRQTVzbUlVSHVZUDFUTTZBUkxTQkppWkZ1NjB6cVhqenFiTFVzTXR0N3V5WGZwNDlmbnFxVWlzR2pCbHl4MGNIQQ&q=https%3A%2F%2Fpan.quark.cn%2Fs%2F39bb114e3214&v=vaCZgu7S2CE) VMware：[https://blogs.vmware.com/teamfusion/2...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbXBZbXRySWR6QXkwWGg4ZzczdWxmQ19NS2lJQXxBQ3Jtc0trRDFLdlh3N21PTGJTNldpcVVTN2huVERQSG1NTFdGNkpGaEhrd3NsaFJlbUVhNmhXTXdpS05qMFNtZGZOakVVaU5PTlRHVXNSUm8yckZqMmtBWi1pcXh0UmxhNzZaSl9scXdUeHpQZFRsV2lXMGRvVQ&q=https%3A%2F%2Fblogs.vmware.com%2Fteamfusion%2F2024%2F05%2Ffusion-pro-now-available-free-for-personal-use.html&v=vaCZgu7S2CE) Ubuntu：[https://ubuntu.com/download/server](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbkxJOVB1YkZxSmkyRTFCUTFQNVduN0NZM0FxZ3xBQ3Jtc0tsa3htaEY2Z3YwSGZXVUdPU1oyXzNhRUdnTGU0VGhXSXhZWlhCZHpmLWp6aE9BMFFzUC1PYTBEUG5SVmJ4cHlxUldEMTd1MVdsYTBRQUdEOGdQS0lfcDQxUFpRckppQWVsZTB2alUwLTVhSERYcTVsTQ&q=https%3A%2F%2Fubuntu.com%2Fdownload%2Fserver&v=vaCZgu7S2CE) 
2. Ubuntu命令： 
	1. 查看内核信息：uname -a 
	2. 安装网络工具包：apt install net-tools 
	3. 查看IP：ifconfig 
	4. ssh命令：ssh 用户名@IP地址 
3. 安装桌面 apt更换清华源： sudo sed -i "s@http://.*archive.ubuntu.com@[https://mirrors.tuna.tsinghua.edu.cn](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa3VybHBpdEx0N2JHOVdpbmdieHBCUjI4LUN1UXxBQ3Jtc0trZGxDbzlsLXpVU0gzTkRCaHBEbFg0UHo5MncyQmlfQVFOOE1zYXpKdi1DeDNZakhxbDFueVA2T2hnLWpubVd6TV9iUDctcXBRM2hqVnZ0azJmRm1McEcwMUdLSUE4d091YjJhSUlYTEdXSUNScjlISQ&q=https%3A%2F%2Fmirrors.tuna.tsinghua.edu.cn%2F&v=vaCZgu7S2CE)@g" /etc/apt/sources.list sudo sed -i "s@http://.*security.ubuntu.com@[https://mirrors.tuna.tsinghua.edu.cn](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbDhzZ2xlRVRXM01LYVpjTDlGM3psdEJZOVdad3xBQ3Jtc0tubmstanJ5TXgtUzh0dkh6LXJxV21qSkQwN2pZb3cxeVZHdEJQcm9DaHdvdloycmwxUS1SeURmbUhLLVo1b2R0UzlEMW1CeWRDaTFFZ1ZFZmF1eFl1a1k2Z3RabnpzNFZSMWJ0ZVlveG85RThTWE55Yw&q=https%3A%2F%2Fmirrors.tuna.tsinghua.edu.cn%2F&v=vaCZgu7S2CE)@g" /etc/apt/sources.list 执行更新 sudo apt update sudo apt upgrade 报错：dpkg was interrupted, you must manually run 'dpkg --configure -a' to correct the problem. 执行：dpkg --configure -a  然后重新执行：sudo apt upgrade 安装Ubuntu desktop：sudo apt install ubuntu-desktop 启用图形界面：sudo systemctl set-default graphical.target 重启系统：sudo reboot
4. **Ubuntu24.04 修改源应该使用`https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu-ports/`否则会报错，无法安装。**

# Mac软件资源网站
1. [awesome-mac](https://wangchujiang.com/awesome-mac/README-zh.html)




![Image](https://mmbiz.qpic.cn/mmbiz_jpg/PfPawcmRR1wWf0n22myAYPZeicfEXYV2s6vmOhQ01G2QKyFnlWib7E06l6IdSrSpleX0lHaiag8Qzy2rAriblEpTgg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



### **MacWk**

🟠一个收录了大量精品Mac软件的网站，包括Adobe全家桶、实用工具、办公软件、图形设计、游戏娱乐等且全都做好了分类，方便按需查找，界面简洁无需登录且完全免费！

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/PfPawcmRR1wWf0n22myAYPZeicfEXYV2sIx3R5uXr1TW4hdhrUc4accVibh4LRTKtVy8icpaJ6PPclKkicAWYKa5dQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



### **Macbl**

🟠页面设计美观大方，独特的插画风格让人耳目一新！无需登录或注册账号直接就可以下载软件，包括媒体音乐、图形设计、软件开发、网络工具、系统工具、行业办公等，支持网盘下载

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/PfPawcmRR1wWf0n22myAYPZeicfEXYV2sSdsZ4hHMXyTg2h2oicA4LjjASiaWTPRtNvJPGicCklxcarSUKhxm0ccicA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### **APPStorrent**

🟠俄罗斯的MacOS免费资源网站，主打一个全面且白嫖！界面简洁无广告，页面默认为俄文但支持切换为中文！基本上可以找到任何你想找的各种类型的Mac软件，无需登录有安装教程，直链下载速度快！

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/PfPawcmRR1wWf0n22myAYPZeicfEXYV2snEMLp31cjWDTTgPrCG5uicPUI9X59raqW04vSWJl8WibTlUchYF9uGSw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### **MACCYY**

🟠这也是一个老牌的Mac软件资源站！没有广告无需注册即可免费下载！同时也做了相应的分类以及中文检索，包括Adobe全家桶、PD虚拟机都能轻松找到，非常的方便！

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/PfPawcmRR1wWf0n22myAYPZeicfEXYV2sia4PnC0DZmQeeXqplTh5n7LbBO0zf7fAPpatk21ezUWWY0BD2WichoRQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### **潘多拉盒子**

🟠页面非常的清晰明了，网站也没有任何的广告！简单注册后即可完全免费下载！按不同功能类型、操作系统、资源类型等分类齐全，并支持直链下载，无任何限制速度非常的快！

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/PfPawcmRR1wWf0n22myAYPZeicfEXYV2sNVDsM16AqicKPY0mHcCs8wLlG9tpbVPTmfw7XR6l2RXVh8CocVlQnhw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# 可能是Linux端最好的听歌体验：Spotify for Linux

![1.png](https://raw.githubusercontent.com/varz1/pics/master/1.png)

一直以来很头疼linux端听音乐的问题，虽然网易云给出了网页端和客户端的解决方案但许多bug也让人不适。偶然发现Spotify有Linux的版本，配合广告屏蔽插件体验出人意料。下面给出Debian / Ubuntu的具体安装体验过程。
## Debian / Ubuntu 安装
详见官方文档[Spotify for Linux](https://www.spotify.com/tw/download/linux/)
如要配合AD block请不要使用snap安装


添加源

 ` $ curl -sS https://download.spotify.com/debian/pubkey.gpg | sudo apt-key add -`      
 `$ echo "deb http://repository.spotify.com stable non-free" |
sudo tee /etc/apt/sources.list.d/spotify.list`

更新源并安装

`$ sudo apt update`

`$ sudo apt install spotify-client`

## 使用
登录时添加代理
`address:127.0.0.1` `port:1080`即可使用
![20200211180205.png](https://raw.githubusercontent.com/varz1/pics/master/20200211180205.png)
如此突兀的广告实在是影响体验，作为一名苦穷学生党只好另寻他路，当然有能力的还是买会员的比较好。推荐github上一款广告屏蔽插件[spotify-adblock-linux](https://github.com/abba23/spotify-adblock-linux#spotify-adblock-linux)

## 插件安装

此处按官方文档给出安装过程

### 所需组件
* gcc
* Make
* libcurl headers (e.g. libcurl4-gnutls-dev on Debian/Ubuntu systems)

    未安装请先安装上述组件

### 编译与安装
先克隆仓库至本地

`$ git clone https://github.com/abba23/spotify-adblock-linux.git`

切换至仓库目录

`$ cd spotify-adblock-linux`

编译

`$ make`

安装

`$ sudo make install`

## 无AD版使用

### 通过命令行打开无AD客户端

` $ LD_PRELOAD=/usr/local/lib/spotify-adblock.so spotify`

### 通过桌面快捷方式打开无AD客户端

切换至目录`~/.local/share/applications`

运行`$ vim Spotify-adblock.desktop`插入内容

`[Desktop Entry]
Type=Application
Name=Spotify (adblock)
GenericName=Music Player
Icon=spotify-client
TryExec=spotify
Exec=env LD_PRELOAD=/usr/local/lib/spotify-adblock.so spotify %U
Terminal=false
MimeType=x-scheme-handler/spotify;
Categories=Audio;Music;Player;AudioVideo;
StartupWMClass=spotify`

保存退出即可看到快捷方式拖动至需要处使用

## 使用体验

个人认为英文界面没有太多障碍。搭配adblock使用后体验感不输网易云。
曲库方面个人使用的Apple music大多歌曲都能找到，中文曲库方面也很给力，周杰伦甚至国内原创rap都能找到。缺点就是可能是本人的问题搜索框无法输入中文还有没有像网易云那样的小窗口模式。
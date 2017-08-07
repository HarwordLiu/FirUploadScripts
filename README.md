# fir自动打包脚本 - - FirUploadScripts

“给我打个debug包，我测个功能点！”
“给我打个release包，我测下线上环境！”
“给我打个。。。。。”

但凡是开发有个一两年的iOS小伙子，以上的这种话肯定是听到吐了。而且如果有过外包公司经历的，更是被配置证书打包之类的问题折磨的疯狂了。

但是！作为一个程序猿，用有限的是生命去做更多的事不是更好，毕竟程序猿是高危物种，说猝死就猝死啊。。。（以上是装逼，纯粹是因为懒，不想用鼠标点来点去。）

我给出的方案是`fir平台+xcodebuild+shell脚本`来进行操作。

本文达成的目标是：终端输入一条命令

```
bash -l ./xcodebuild_dis_config.sh
```

回车喝杯茶，自动打包上传fir。

### 那么我们开始吧

#### 一 准备环境和资源

首先说下所需要的环境：`Xcode8.3` `fir` 以及系统的`rvm`

贴一下`fir`的安装方式，也可以去他们官网的[`GitHub`](https://github.com/FIRHQ/fir-cli/blob/master/doc/install.md)去查看。使用的是`ruby`来进行的安装：

```
$ ruby -v # > 1.9.3
$ gem install fir-cli
```

其次在fir的官网申请账号并在个人中心获取`API Token`记下来。

[`fir官网`](https://fir.im/)


#### 二 配置证书

这一部分我就不详细介绍了，因为网上一搜一大堆。

我这里主要说下我们需要把什么记下来，首先登陆你的开发者账户

![](http://orsg2lmcy.bkt.clouddn.com/QQ20170807-212632.png/600)

在`memberShip`栏目中记下`Team ID`

#### 三 下载脚本

题主已经将对应写好的脚本上传到了`GitHub`，`clone`到本地然后将工程下的`scripts`文件夹拖到项目的根目录下。

[GitHub下载地址](https://github.com/HarwordLiu/FirUploadScripts)

工程结构举例如图：

![](http://orsg2lmcy.bkt.clouddn.com/QQ20170807-213243.png/600)

#### 四 脚本内的文件配置

脚本内文件为

![](http://orsg2lmcy.bkt.clouddn.com/QQ20170807-213601.png/600)

首先从命名就能看出可以分为两套，一套对应的是`development`的打包脚本，一套对应的是`distribution`的打包脚本。

`.sh`里面对应的写好的脚本，`plist`里面对应的是相应的打包时对应的xcodebuild的配置文件。

##### 关于`.sh`

这里就不把详细的脚本贴出来了，我只贴出来对应的需要我们进行配置的参数解释：

![](http://orsg2lmcy.bkt.clouddn.com/QQ20170807-214310.png/600)

根据之前的贴图进行举例如下：

![](http://orsg2lmcy.bkt.clouddn.com/QQ20170807-214714.png/600)

我们也可以自己自定义对应的更新日志，这个在脚本的最后进行配置。

##### 关于`.plist`

![](http://orsg2lmcy.bkt.clouddn.com/QQ20170807-215128.png/600)

`Team ID`就是前文提到需要记录的开发者账户的`Team ID`

`method`对应的打出什么种类的包，有效值有4个，对应手动打包的那几个选项：
```
app-store,
ad-hoc,
enterprise,
development
```

那么对应的我们在打`development`的包的时候在对应的脚本的.plist里面填写`development`，这里相信是很简单的就不过多赘述了，
如果对xcodebuild的plist配置想要详细研究，脚本也贴出了对应的key值都是用来干什么的，可以看一下。

#### 五 配置到这里，就完成了

那么接下来该怎么做呢？

产品："那个谁谁谁，给我打个debug包！"

🐒 ："知道了~"

打开`Terminal`

```
$ cd 工程目录/scripts/

$ bash -l ./xcodebuild_dis_config.sh
```

打包上传一气呵成，然后我们就可以喝茶去了。

##### 总结

其实这个脚本还不是很完善，比如针对多工程，多target的工程，还需要进行特殊的处理，但是折腾是永无止境的。等以后抽时间再去弄弄。让自己的时间都用在有价值的事情上，才是我们折腾的最终目的。比如在这个脚本中还可以添加自动发邮件，将邮件直接发给产品测试大兄弟，这样你连QQ通知都省了。

最后，还是老规矩贴出博主的私人博客[@HarwordLiu](https://harwordliu.com)

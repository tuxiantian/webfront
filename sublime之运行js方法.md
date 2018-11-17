小伙伴一直对我的 ST 能直接运行js感到非常好奇，今天我就公布下这个“秘密”吧。。
![img](http://images.cnitblog.com/i/477954/201406/242212358463555.jpg)
其实非常简单，配置个编译系统即可。
可是编译系统是什么，怎么配置呢？
接下来我一步一步教你吧。。
(好像有人告诉我说有什么插件可以实现的，不过还是有noedjs的。。)
PS: 其实微软也有对 js 的实现叫做 JScript，windows下可基于 WSH 运行，不过还是 nodejs 给力。。



首先，我们下载 [nodejs](http://nodejs.org/) 这个是必备的，做为一个合格的前端，肿么能没有node呢？
哪怕你不会用，装一个装逼也是极好的。。
如果第一次接触这东西，一直点下一步就安装好了。

我们打开 cmd 看看是否能安装成功。
还记得怎么打开cmd么？
**win+r** 或者点 **开始->运行** 输入 cmd 即可。
然后输入 node -v 看看是否安装成功了。
![img](http://images.cnitblog.com/i/477954/201406/242213202671959.jpg)
看到一个版本号，说明安装成功，可以正常运行了。。
接下来打开你的神器 ST 吧。
选择菜单 **Tools --> Build System --> new Build System...** 
中文版的话是 **工具 --> 编译系统 --> 新建编译系统...![img](http://images.cnitblog.com/i/477954/201406/242214058461051.jpg)**

然后写入下面内容:

```javascript
{
    "cmd": ["node", "$file"],
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "working_dir": "${project_path:${folder}}",
    "selector": "source.js",
    "shell": true,
    "encoding": "utf-8",
    "windows": {
        "cmd": ["taskkill /f /im node.exe >nul 2>nul & node", "$file"]
    },
    "linux": {
        "cmd": ["killall node; node", "$file"]
    }
}
```

接着保存为 javascript.sublime-build，保存位置默认即可。

现在，我们在桌面新建一个 test.js 试试吧，写个简单的测试代码后按 Ctrl + B 或者 F7 运行。
![img](http://images.cnitblog.com/i/477954/201406/242213527991798.jpg)
成功了。。

其实网上有很多教程，但是不少朋友说有点小问题，
比如一定要选择刚才新建的 javascript 编译系统才能执行。
其实是因为网上很多地方把 "selector": "source.**js**", 写成了 "selector": "source.**javascript**",
这样他就不能根据 **后缀名** 自动选择编译系统了。

还有很多人运行后得到的结果是乱码，其实这个问题确实不容易解释。。
但是我可以告诉你怎么调。
看到 "encoding": "utf-8", 这个了吧，现在是 utf-8 如果你遇到乱码的情况，改成 gbk 即可。
 
有朋友遇到执行后输出

[Decode error - output not utf-8]
[Finished in 1.0s with exit code 1]
这个错误的意思是 输出的不是 utf-8 的，改成 "encoding": "gbk" 看看出什么错误了。

不同的错误处理方法不同。
这种错误往往是控制台报错导致的。。
如果你是 ST3 的话建议改下这里
"cmd": ["taskkill /f /im node.exe >nul 2>nul & node", "$file"]
改成
"cmd": ["node", "$file"]
试试先。

**2014-07-09 更新=========**

有一个问题要注意下，被执行的文件路径不能出现中文，也就是说 xp 下，放在桌面上是执行不了的，因为路径里有 “桌面” 两中文字符。
win8 貌似没事，桌面的路径是 C:\Users\用户名\Desktop\ 只要用户名是英文的，就不会有问题了。
以防万一，放在D盘下执行最好了。

还有朋友发现 windows 2003 下运行不了，我也不知道怎么回事。

在 XP(32位) Win7(32位) Win8.1(64位) 下都测试了，没问题的，也许是个例吧。。

'node' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
[Finished in 0.2s with exit code 1]
注意到最后一步记得（重启sublime）不然会出现上面这个错误
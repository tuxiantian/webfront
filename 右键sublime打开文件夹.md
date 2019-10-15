1，安装Sublime

2，按ctrl + r，输入regedit，回车，打开注册表编辑器

3，找到以下路径：计算机/HKEY_CLASSES_ROOT/Folder/shell

4，右键shell，新建 “项”，命名随意，比如 openwithsublime

5，选中 openwithsublime，双击右侧 “（默认）”，修改 “数值数据”，比如“从Sublime打开”，这是显示在右键菜单的选项名字，随意

6，选中 openwithsublime，右键新建“项”，命名“command”，这个不能随意

7，选中新建的command，双击右侧“（默认）“，修改”数值数据“，比如”C:\Program Files\Sublime Text 3\subl.exe %1“，这是点击右键选项后执行的命令，前面是执行文件在电脑中的绝对路径，后面是命令参数，%1表示当前选中的文件夹路径

8，回车，这是即时生效的，找一个文件夹右键试试看
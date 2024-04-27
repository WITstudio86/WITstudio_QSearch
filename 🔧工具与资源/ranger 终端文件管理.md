## 使用

直接在终端输入`ranger`即可进入ranger模式  

![](https://pic3.zhimg.com/80/v2-d72c823c9c68123b91c1f30a9247f1fa_1440w.webp)

Image

  

## 快捷键

在浏览时常用的快捷键

```text
S   切换到ranger最后浏览的目录
zh/退回键  显示隐藏文件
H   后退
L   前进
gg  跳到顶端
G   跳到底端
gh  go home
gn  新建标签(tab键切换标签)
f   查找(如果只有一个匹配结果会直接打开该目录或文件)
/   搜索
g   快速进入目录
```

这些快捷键都是与`vim`的操作一样

```text
yy      复制
dd      剪切
pp      粘贴
dD      删除（需要回车键确认）
cw      重命名
A       在当前名称基础上重命名
I       类似A, 但是光标会跳到起始位置
Ctrl-f  向下翻页
Ctrl-b  向上翻页
```

书签

```text
m       新建书签
`       打开书签
um      删除书签
```

标签

```text
gn / Ctrl-n        新建标签
TAB / Shift-TAB     切换标签
gc / Ctrl-w        关闭标签
```

文件排序 :

```text
on/ob   根据文件名进行排序(natural/basename)
oc      根据改变时间进行排序 (Change Time 文件的权限组别和文件自身数据被修改的时间)
os      根据文件大小进行排序(Size)
ot      根据后缀名进行排序 (Type)

oa      根据访问时间进行排序 (Access Time 访问文件自身数据的时间)
om      根据修改进行排序 (Modify time 文件自身内容被修改的时间)
```

## 安装插件

`ranger`也有很多预览时用的插件

```text
macOS
brew install libcaca highlight atool lynx w3m elinks poppler transmission mediainfo exiftool

ubuntu
sudo apt-get install caca-utils # img2txt 图片
sudo apt-get install highlight  # 代码高亮
sudo apt-get install atool　    # 存档预览
sudo apt-get install w3m        # html页面预览
sudo apt-get install mediainfo  # 多媒体文件预览
sudo apt-get install catdoc     # doc预览
sudo apt-get install docx2txt   # docx预览
sudo apt-get install xlsx2csv   # xlsx预览
```

最后总结一下：

- `g`开头主要是`目录跳转`，后面可以跟一些参数指定要跳转的位置
- `s`开头主要是`排序`，后面跟一些排序规则
- `z`开头主要是`设置`，后面跟一些具体要设置什么
- `.`开头主要是`文件过滤`，后面跟一些过滤规则筛选出满足条件的文件或目录

## 配置
ranger默认情况下不会生成配置文件，需要手动生成（拷贝）：

```text
ranger --copy-config=all
```

这个时候ranger就会生成配置文件目录~/.config/ranger，下面主要有这样几个文件：

```text
rc.conf     - 选项设置和快捷键
commands.py - 能通过 : 执行的命令
rifle.conf  - 指定不同类型的文件的默认打开程序。
scope.sh    - 用于指定预览程序的文件
```

首先得设置一下文件关联，系统自带的文件关联存在一些问题，其中最主要就是一些自定义文件类型不是很好识别，这个时候最好直接采用系统默认的程序打开，尤其是doc文件。

```text
#找出含有docx的一行，然后将其注释起来：
#ext docx?, has catdoc,       terminal = catdoc -- "$@" | "$PAGER"

has xdg-open, flag f = xdg-open "$1"
```

这样对于很多扩展文件即可使用系统默认的程序打开了。  
然后再修改scope.sh文件，在合适的位置（就是代码相似的位置）添加如下代码：

```text
    # Doc documents
    doc)
        try catdoc "$path" &&amp; { dump | trim | fmt -s -w $width; exit 0; }|| exit 1;;
    # Docx documents:
    docx)
        try docx2txt < "$path" &&amp; { dump | trim | fmt -s -w $width; exit 0; }|| exit 1;;
    # Xlsx documents:
    xlsx)
        try xlsx2csv "$path" &&amp; { dump | trim | fmt -s -w $width; exit 0; }|| exit 1;;
```

不过很明显的，上述配置仅仅添加了doc、docx、xlsx三种文件预览方式，而对于ppt,pptx以及其它的文件，也可以通过转换成文本的来实现文件预览。

## **四、功能配置**

## **4.1 删除配置**

ranger并没有自带删除的快捷，所以需要手动配置一下．一般情况下，最好使用trash-cli作为删除的命令(相对rm来说要可靠安全得多).  
在打开~/.config/ranger/rc.conf文件，然后在最后面添加

```text
map D shell trash %s
```

即可实现用”D”将当前所选文件放到trash-bin中去.

## **4.2 解压缩配置**

编辑~/.config/ranger/commands.py文件，添加下面行到文件尾，实现:extract解压选中文件.

```text
class extract(Command):
    """:extract <paths>
    Extract archives
    """
    def execute(self):
        import os
        fail=[]
        for i in self.fm.thistab.get_selection():
            ExtractProg='7z x'
            if i.path.endswith('.zip'):
                # zip encoding issue
                ExtractProg='unzip -O gbk'
            elif i.path.endswith('.tar.gz'):
                ExtractProg='tar xvf'
            elif i.path.endswith('.tar.xz'):
                ExtractProg='tar xJvf'
            elif i.path.endswith('.tar.bz2'):
                ExtractProg='tar xjvf'
            if os.system('{0} "{1}"'.format(ExtractProg, i.path)):
                fail.append(i.path)
        if len(fail) > 0:
            self.fm.notify("Fail to extract: {0}".format(' '.join(fail)), duration=10, bad=True)
        self.fm.redraw_window()
```

很明显，上面少了很多压缩包的解压方式，如rar之类的，但是可以按照格式，自行添加相应的解压命令．

## **4.3 压包设置**

同样的，将下面内容复制到~/.config/ranger/command.py的末尾，即可实现:compress压缩选中的文件．

```text
import os
from ranger.core.loader import CommandLoader

class compress(Command):
    def execute(self):
        """ Compress marked files to current directory """
        cwd = self.fm.thisdir
        marked_files = cwd.get_selection()

        if not marked_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        original_path = cwd.path
        parts = self.line.split()
        au_flags = parts[1:]

        descr = "compressing files in: " + os.path.basename(parts[1])
        obj = CommandLoader(args=['apack'] + au_flags + \
                [os.path.relpath(f.path, cwd.path) for f in marked_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

    def tab(self):
        """ Complete with current folder name """

        extension = ['.zip', '.tar.gz', '.rar', '.7z']
        return ['compress ' + os.path.basename(self.fm.thisdir.path) + ext for ext in extension]
```

同样的，上面也只支持上面四种压缩方式，对于其它的压缩方式，需要自行添加．
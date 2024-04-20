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
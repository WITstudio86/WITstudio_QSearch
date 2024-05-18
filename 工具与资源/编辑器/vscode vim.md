## 使用

vim 提供了 3 个基本模式：normal ， insert , visual。

- normal模式：就是 vim 的普通模式，不需要知道这个模式是干嘛，只需要找到这个模式下可以做很多事情就行了。
- insert模式：插入模式，在 normal 模式下按 i 就可以进入这个模式，这个模式跟没装 vim 时差不多，可以直接编码，按 ESC 可以回到 normal 模式。
- visual模式：这个模式可以进行文本选择，normal模式下按 v 进入，按 V 进入并选择一整行。

下面简单介绍下一些用法：

### normal模式

h左 j下 k上 l右 这移动方向键就不多说了

- x：删除当前字符
    
- w：向后移动一个单词
    
- b：往前移动一个单词
    
- e：移动到单词结尾
    
- dw： 删除一个单词
    
- cw： 删除一个单词并进入 insert 模式
    
- gg: 到文件头部。
    
- G: 到文件尾部。
    
- dd：删除一整行
    

各种翻屏操作：

- ctrl+f: 下翻一屏。
    
- ctrl+d: 下翻半屏。
    
- ctrl+b: 上翻一屏。
    
- ctrl+u: 上翻半屏。
    
- zz: 将当前行移动到屏幕中央。
    
- zt: 将当前行移动到屏幕顶端。
    
- zb: 将当前行移动到屏幕底端。
    

写了一点发现 Vim 的使用指令实在是太多了，详情入门教程可以通过这个学习：[简明 VIM 练级攻略](https://coolshell.cn/articles/5426.html)

一定要勤加练习，抛弃原有的编码习惯，用习惯了 vim，就是一个字 贼爽。

## 进阶

### vim-easymotion

用久了 vim， 你还会发现 其实hjkl和wb的移动有些时间还是有点难受的。这时候你就可以用一个神器了—— vim-easymotion，人如其名：让移动更加简单。 进入 setting.json 增加如下几行

```
  "vim.easymotion": true,
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": [" "],
      "after": ["leader", "leader", "leader", "b", "d", "w"]
    }
  ],
```

然后回到文件中，按下空格，就会发现编辑器显示区域的所有单词前头，都会显示出一个或者两个字符。![ZhsLmU](https://md-1252929012.cos.ap-guangzhou.myqcloud.com/uPic/ZhsLmU.png)按下字符，就可以快速跳转到该单词位置。是不是非常便利的跳转！爸爸妈妈再也不用担心我疯狂hjklwb了。

### VSCode vim 使用技巧

- gd：Go to definition, 跳转到定义。
- ctrl + o: 跳转之后退回。
- gb：找出与光标下相同的下一个单词, 并添加一个光标 ，接下来就可以同时修改。
- af：VISUAL 模式命令, 依据语法分析, 将选择区域向外扩展。
- gh：等同于将鼠标移至光标所在单词, 方便查看定义以及报错。

## 解决烦人的拼音问题

在insert模式下如果是中文输入法，切换到normal模式默认还是中文输入，所以移动jk 会出现拼音提示，需要手动切换才能消除。 vscode vim 官方也给出了解决方案，可以自动完成切换过程。

1. 安装 im-select: [Switch your input method from terminal](https://github.com/daipeihust/im-select)
2. 进行settings.json配置修改

```
"vim.autoSwitchInputMethod.enable": true,
  "vim.autoSwitchInputMethod.defaultIM": "com.apple.keylayout.ABC",
  "vim.autoSwitchInputMethod.obtainIMCmd": "/usr/local/bin/im-select",
  "vim.autoSwitchInputMethod.switchIMCmd": "/usr/local/bin/im-select {im}",
```
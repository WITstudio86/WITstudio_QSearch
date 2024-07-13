## 安装插件

我只需要两个插件：

- `zsh-autosuggestions`：这个是自动建议插件，能够自动提示你需要的命令。 ~~已经使用 [atuin](atuin.md)代替~~ 不代替 , 一起使用
- `zsh-syntax-highlighting`：这个是代码高亮插件，能够使你的[命令行](https://www.zhihu.com/search?q=%E5%91%BD%E4%BB%A4%E8%A1%8C&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A%22345559097%22%7D)各个命令清晰明了。
- `autojump` : 快速去到曾经去过的地址 , j + 大概路径即可

可以直接通过 homebrew 下载

## 启用插件

打开 `~/.zshrc` 文件，将以下行代码添加到其中：

```shell
%% 已经使用 atuin代替 %%
source /usr/local/Cellar/zsh-autosuggestions/0.7.0/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/local/Cellar/zsh-syntax-highlighting/0.8.0/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/local/Cellar/autojump/22.5.3_3/share/autojump/autojump.zsh
```

  > 具体地址在使用 brew 安装的时候可以看到
  
> 完整的工作流还包含: [ranger 终端文件管理](工作流/ranger%20终端文件管理.md) [startship终端](工作流/startship终端.md) [zellij终端复用](工作流/zellij终端复用.md)


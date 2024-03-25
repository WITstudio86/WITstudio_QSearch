# Rust 写的高颜值终端

- 官网: [Starship](https://starship.rs/zh-cn/guide/)
- 源码: [Starship](https://starship.rs/zh-cn/guide/)

## 字体安装

- [Nerd Fonts - Iconic font aggregator, glyphs/icons collection, & fonts patcher](https://www.nerdfonts.com/font-downloads)
- 下载对应的字体 , 苦茶甜橘喜欢用 JetBrainsMono Nerd Font
- 下载后再终端设置中启用字体 , 

## 安装

macos 安装

```shell
curl -sS https://starship.rs/install.sh | sh
```

## 启用

zsh 中启用

```shell
vi ~..zshrc
```

添加内容

```
eval "$(starship init zsh)"
```

## 完成
新建终端实例即可
# atuin
终端历史命令复用工具
[Atuin - Magical Shell History](https://atuin.sh/)

## 下载
```shell
brew install atuin
```

## 快速使用

```
%% 下载默认设置 %%
bash <(curl --proto '=https' --tlsv1.2 -sSf https://setup.atuin.sh)

%% 如果需要云同步的话执行下面的指令 %%
atuin register -u <USERNAME> -e <EMAIL>
atuin import auto
atuin sync
```

> 用户名密码需要注册: [login](https://docs.atuin.sh/guide/sync/#login)
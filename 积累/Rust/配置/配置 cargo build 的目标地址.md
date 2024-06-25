
- 在`~/.cargo` 下创建`config` 文件 
- 修改内容

```toml
[build]
target-dir = "/Users/wuzexian/codes/.target"
```

> `target-dir` 设置的就是所有通过`cargo build` 生成的编译结果所存储的地址
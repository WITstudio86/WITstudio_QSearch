我的配置:

```toml
# 样式配置 参考: https://github.com/alacritty/alacritty-theme
import = [
    "~/.config/alacritty/themes/themes/everforest_dark.toml"
]

[font]
size = 16.0

[font.bold]
family = "JetBrainsMono Nerd Font"
style = "Bold"

[font.bold_italic]
family = "JetBrainsMono Nerd Font"
style = "Bold Italic"

[font.italic]
family = "JetBrainsMono Nerd Font"
style = "Italic"

[font.normal]
family = "JetBrainsMono Nerd Font"
style = "Regular"

[keyboard]
# 生成新实例(窗口)
bindings = [
   { key = "Return", mods = "Control|Shift", action = "SpawnNewInstance" }
]


[window]

opacity = 0.9
dimensions = { columns = 120, lines = 30}
padding = { x = 20, y = 10}
decorations = "none"
```
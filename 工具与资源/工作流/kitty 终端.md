- 配置文件:
```
# BEGIN_KITTY_THEME
# Everforest Dark Hard
include current-theme.conf
# END_KITTY_THEME
#

# font
font_size 20
font_family         JetBrainsMono Nerd Font Mono SemiBold
bold_font           JetBrainsMono Nerd Font Mono Bold
italic_font         JetBrainsMono Nerd Font Mono Italic
bold_italic_font    JetBrainsMono Nerd Font Mono Bold Italic


# window ui
# 设置成 yes 可以关闭圆角
hide_window_decorations       titlebar-only
# 文字到边框的距离
window_padding_width          10
# 背景透明度
background_opacity            0.8
# dynamic_background_opacity    True
# allow_remote_control          yes
# 背景模糊
background_blur               30
# 记忆上退出的窗口尺寸
remember_window_size          yes


# bar
# bar 的位置
tab_bar_edge                top
# 风格
tab_bar_style               powerline
tab_powerline_style         slanted



# 快捷键绑定
# map 快捷键组合 行为 什么时候启用 具体内容
# mao cmd+s send_text all \e:w\r
map super+u remote_control set-background-opacity --toggle 1

# 选中复制
copy_on_select yes
```
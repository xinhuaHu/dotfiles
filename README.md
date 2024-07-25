`Archlinux hyprland` 的 `.config`

| 文件夹 | 说明 |
| --- | --- |
| hypr | hyprland 的配置文件包括样式的主题 |
| kitty | 终端配置文件 |
| mako | 通知样式 |
| waybar | waybar 的配置和主题文件 |
| wofi | wofi 的配置文件 |
| yazi | 使用 [config](https://github.com/cap153/config) 的是 yazi 文件夹内容  |

桌面背景使用的是 `swaybg` 使用 `shell` 脚本进行切换，脚本文件统一保存在 `~/script` 文件夹下

`random_wallpaper.sh`

```bash
#!/bin/sh
swaybg -i $(find /home/arch/Pictures/wallpaper -type f | shuf -n1) -m fill &
OLD_PID=$!
while true; do
    sleep 600
    swaybg -i $(find /home/arch/Pictures/wallpaper -type f | shuf -n1) -m fill &
    NEXT_PID=$!
    sleep 5
    kill $OLD_PID
    OLD_PID=$NEXT_PID
done
```

在 `hypr` 的配置文件中的 `USER EXEC` 是用户的启动项配置，其中 `exec-once = echo 'Xft.dpi: 120' | xrdb -merge` 是用于配置屏幕缩放的
```
#############################
###       USER EXEC       ###
#############################

exec-once = waybar & ~/script/random_wallpaper.sh
exec-once = fcitx5 --replace -d
exec-once = echo 'Xft.dpi: 120' | xrdb -merge
```

这部分是配置双显示器的，如果有多显示器可以参考

```
################
### MONITORS ###
################

# See https://wiki.hyprland.org/Configuring/Monitors/
# monitor=,preferred,auto,auto
monitor=eDP-1,preferred,auto,1
monitor=HDMI-A-2,highres,auto,1
```
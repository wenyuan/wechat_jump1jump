# 造轮子系列：用 Python 来玩微信跳一跳
## 源码来自原作者[wangshub](https://github.com/wangshub/wechat_jump_game)

## 原理说明

1. 将手机点击到《跳一跳》小程序界面
2. 用 ADB 工具获取当前手机截图，并用 ADB 将截图 pull 上来
```shell
adb shell screencap -p /sdcard/autojump.png
adb pull /sdcard/autojump.png .
```
3. 计算按压时间
  * 手动版：用 Matplotlib 显示截图，用鼠标先点击起始点位置，然后点击目标位置，计算像素距离；
  * 自动版：靠棋子的颜色来识别棋子，靠底色和方块的色差来识别棋盘；
4. 用 ADB 工具点击屏幕蓄力一跳
```shell
adb shell input swipe x y x y time(ms)
```
## 项目依赖

## 使用教程

- 方法 1：使用 app 进行一键操作。目前已适配 Win10 64位/macOS 平台 Android 一键操作，下载请移步 [STOP_jump](https://github.com/wangshub/wechat_jump_game/releases)

- 方法 2：相关软件工具安装和使用步骤请参考 [Android 和 iOS 操作步骤](https://github.com/wangshub/wechat_jump_game/wiki/Android-%E5%92%8C-iOS-%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4)

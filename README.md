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

## 使用教程
1. 我是用的安卓机进行调试的,所以这里记录我的调试步骤
2. ADB环境搭建
   - Android 或 Android 模拟器需要使用 ADB 进行连接
   ADB驱动，可以到[这里](https://adb.clockworkmod.com/)下载</br>
   不过我使用的是[绿色版](http://adbshell.com/downloads),下载完直接解压,然后配置环境变量,在Path里添加ADB开发工具的所在路径,这里我的是 `D:\adb;`
   - 打开windows的cmd命令窗口,输入 `adb` 按回车,如果显示很多adb的命令你的adb环境变量就配置成功了
3. 我的是Windows系统,如下配置
   - 安装Python 2.7/3
   - 安装完后插入安卓设备且安卓已打开 USB 调试模式，终端输入 `adb devices` ,显示如下表明设备已连接
        ```
        List of devices attached
        6934dc33    device
        ```
   - 部分新机型可能需要再另外勾上**允许模拟点击**权限
   - 小米设备除了 USB 调试，还要打开底下的 USB 调试（安全）
   - USB 可能要设置成 MTP(传输文件) 模式
4. 安装依赖文件
    ```
    pip install -r requirements.txt
    ```
5. 界面转至微信跳一跳游戏，点击开始游戏
6. 请按照你的机型或手机分辨率从 `./config/` 文件夹找到相应的配置，把对应的 `config.json` 拷贝到项目根目录，与 *.py 同级
   - 如果屏幕分辨率能成功探测，会直接调用 config 目录的配置，不需要复制
   - 优先按机型去找，找不到再按分辨率
   - 如果都没有请找一个接近的自己的分辨率，或者调节一下找到合适的参数
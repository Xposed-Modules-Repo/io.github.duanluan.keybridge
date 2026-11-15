# KeyBridge

在指定远控或容器 App 位于前台时，把物理键盘的组合键交给前台 App，而不是由 Android
系统处理。适合 RustDesk、网易 UU 远程、TeamViewer、AnyDesk、向日葵、ToDesk、
Moonlight、小小电脑、Tiny Container 等场景。

默认组合键为 `Alt+Tab` 和 `Cmd+D`，可以在 KeyBridge 界面里添加其他组合，例如 `Cmd+F`。

## 要求

- Android 8.1 及以上（minSdk 27）
- Magisk 或 KernelSU
- Zygisk（例如 ZygiskNext）
- Vector 或兼容的 Xposed 框架

## 安装

1. 安装 `KeyBridge-1.0.apk`。
2. 在 Xposed 管理器中启用模块。
3. 把作用域设为 **system**（Vector CLI 使用 `system/0`）。
4. 重启设备。
5. 打开桌面上的 **KeyBridge**，确认组合键列表。

## 使用

- 点击“添加组合键”，然后直接按下要转发的组合，例如 `Cmd+F`。
- 组合键只在 allowlist 内的 App 前台时转发；平板桌面、设置等界面仍保留系统快捷键。
- KeyBridge 界面本身也在 allowlist 内，可以直接在界面里测试组合键。
- 捕获等待期间会消费所有按键，避免误触系统快捷键；按 Esc 取消。

默认 allowlist：

```
com.carriez.flutter_hbb                  # RustDesk
com.netease.uuremote                     # 网易 UU 远程
com.anydesk.anydeskandroid               # AnyDesk
com.oray.sunlogin                        # 向日葵控制端
com.teamviewer.teamviewer.market.mobile  # TeamViewer 控制端
com.teamviewer.quicksupport.market       # TeamViewer QuickSupport
youqu.android.todesk                     # ToDesk
com.aomei.anyviewer                      # AnyViewer
com.example.raylink_flutter              # RayLink
ry.asklink.mobile                        # AskLink
cn.crossdesk.mobile                      # CrossDesk
com.hoptodesk.app                        # HopToDesk
com.limelight                            # Moonlight
com.meshdock.mobile                      # MeshDock
com.fct.tiny                             # 小小电脑（Tiny Container v1）
com.fct.tc4                              # Tiny Container 4 / 小小电脑新版
```

组合键和启用状态保存在模块自己的 `files/combos.json`。修改后立即生效，不需要重启。

## 注意

- 模块会 hook `PhoneWindowManager` 和 Samsung `PhoneWindowManagerExt` 的
  `interceptKeyBeforeDispatching`。出现按键异常时，先禁用模块并重启。
- 如果键盘固件把 `Cmd+D` 直接发成 `KEYCODE_HOME`，系统无法区分它和普通 Home 键，
  模块无法拦截。
- 模块只在 allowlist 内的 App 前台时生效；如果前台包名识别失败，默认不拦截。
- 如果 Manjaro 分支或其他定制版修改了 `applicationId`，需要把新包名加入 allowlist。

## 源码

https://github.com/duanluan/KeyBridge

版本：1.0（versionCode 1）

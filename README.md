[README.md](https://github.com/user-attachments/files/27172100/README.md)
# NBWindows

为 macOS Dock 带来 Windows 风格的任务栏交互体验——点击当前前台 app 的 Dock 图标，即可最小化窗口；再次点击还原。

> 🪟 一个轻量的 macOS 小工具，单 Swift 文件，无任何第三方依赖。

## 功能一览

- **Windows 风格 Dock 点击** — 前台 app 的 Dock 图标一点即最小化，再点还原
- **悬浮窗口栏** — 屏幕顶部半透明面板，列出所有有窗口的 app，点击切换最小化/还原；支持右键关闭/排除，拖拽移位，锁定位置
- **Dock 状态指示灯** — 每个 app 的 Dock 图标上方显示彩色圆点：🟢 窗口可见，🟠 已最小化
- **App 排除** — 右键悬浮栏中的 app 可隐藏，随时从菜单栏恢复
- **位置记忆** — 悬浮栏位置重启后保持不变

## 系统要求

- macOS 13 Ventura 及以上
- **关键：需要辅助功能权限**（首次启动时会弹出授权提示）

## 安装（给首次使用的用户）

### 快速安装（推荐）

1. 打开 `NBWindows.dmg`
2. **先双击「安装 NBWindows.command」**——它会自动完成：复制 app 到 `/Applications/` → 解除 macOS 隔离 → 启动 app
3. 按系统提示，前往 **系统设置 → 隐私与安全性 → 辅助功能**，找到 `NBWindows` 并**勾选** ✅
4. 完成！以后双击 `NBWindows.app` 即可启动

### 手动安装

```bash
cp -r NBWindows.app /Applications/
xattr -dr com.apple.quarantine /Applications/NBWindows.app
open /Applications/NBWindows.app
```

然后按提示授权辅助功能权限。

## ⚠️ 重要注意事项

### 🔑 辅助功能权限

NBWindows 需要辅助功能权限才能拦截 Dock 点击和操作窗口。请在 **系统设置 → 隐私与安全性 → 辅助功能** 中确保 `NBWindows` 已被勾选。

如果勾选后仍不生效，可以查看日志确认：
```bash
tail -f /tmp/nbw*.log
```
如果看到 `AXIsProcessTrusted=false`，说明权限未正确授予。

### 🔄 授权后仍不能用？请重启！

**如果已经授权了辅助功能，但点击 Dock 图标仍然没有反应，请先尝试以下操作：**

1. 退出 NBWindows（点击菜单栏图标 → 退出）
2. **重启电脑**，或者**注销后重新登录**
3. 重新打开 NBWindows

> 为什么需要重启？macOS 对辅助功能权限的授权会在 app 启动时缓存，授权需要在 app **重启之后**（有时甚至在系统重启之后）才能生效。这是一个 macOS 系统的已知行为，不是 bug。

### 🔁 重新构建后权限失效

如果你从源码重新构建 NBWindows，必须使用 `--identifier "com.nb.windows"` 签名，否则 macOS 会认为这是一个新 app，辅助功能权限会失效，需要重新授权。

使用 `build.sh` 脚本构建可以自动处理这个问题。

## 使用方法

| 操作 | 效果 |
|---|---|
| 点击前台 app 的 Dock 图标 | 最小化窗口 |
| 点击已最小化 app 的 Dock 图标 | 还原窗口 |
| 点击悬浮栏中的 app 图标 | 切换最小化 / 还原 |
| 右键悬浮栏中的 app 图标 | 关闭窗口 / 排除此 app |
| 拖拽悬浮栏 | 移动位置 |
| 点击悬浮栏锁图标 | 锁定 / 解锁位置 |
| 点击菜单栏图标 | 开关指示灯、开关悬浮栏、调整位置、退出 |

## 常见问题

**点击 Dock 没有反应** — 检查辅助功能权限。查看日志：`tail -f /tmp/nbw*.log`。

**指示灯不显示** — 点击菜单栏图标，确认「程序坞状态灯」已勾选。

**悬浮栏不见了** — 点击菜单栏图标 → 位置 → 选择任意预设位置即可找回。

**已经授权了但依然不工作** — 如上所述，请重启电脑或注销重登录。

## 从源码构建

```bash
xcode-select --install
bash /Applications/NBWindows.app/Contents/Resources/build.sh
```

## 项目结构

```
NBWindows.app/
└── Contents/
    ├── Info.plist
    ├── MacOS/
    │   └── NBWindows
    └── Resources/
        ├── main.swift         # 全部源码（~1000 行）
        ├── build.sh           # 一键构建 + 签名 + 重启
        └── README.md
```

## License

MIT

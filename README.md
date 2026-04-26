[README.md](https://github.com/user-attachments/files/27101857/README.md)
# NBWindows 🪟

> 一个轻量级的 macOS 窗口管理器悬浮栏，实时显示当前有窗口的应用

![NBWindows 截图](https://via.placeholder.com/600x80/1a1a1a/ffffff?text=NBWindows)

## 为什么需要它？

macOS 的 Dock 和调度中心不够直观：

- **点了 ❌ 关闭的应用** → Dock 里图标还在，但你知道它有没有窗口吗？
- **最小化的应用** → 调度中心不显示
- **桌面一堆窗口** → 有时候根本不知道哪些程序开着

**NBWindows** 用一个悬浮栏清晰告诉你：**当前哪些应用真的有窗口**。

## 功能

- 🔲 **悬浮栏** — 显示所有有窗口的应用图标（含最小化的）
- 🅧 **点 ❌ 关闭的应用不显示** — 只显示真正有窗口的
- 🔄 **左键切换** — 在前时最小化，不在前时聚焦到前（Windows 风格）
- 🖱️ **右键关闭** — 右键图标 → 关闭窗口（和点红 × 一样，不退出应用）
- 🔒 **锁按钮** — 锁定/解锁悬浮栏位置
- 🟢🟠🔵 **状态指示** — 右下角颜色条标明窗口状态
- ↕️ **拖拽任意位置** — 想放哪放哪，位置记忆
- 🚀 **跨空间** — 所有桌面空间都能看到

## 安装

### 直接使用

下载 `NBWindows.app`，拖到「应用程序」文件夹，打开即可。

> ⚠️ **首次使用**：需要授予辅助功能权限
> 系统设置 → 隐私与安全性 → 辅助功能 → 添加 NBWindows.app

### 自行编译

```bash
# 需要 Xcode Command Line Tools
git clone [你的仓库地址]
cd NBWindows
swiftc -o NBWindows main.swift
# 或者直接 open NBWindows.app（如果已打包）
```

## 管理

```bash
# 启动
open /Applications/NBWindows.app

# 停止（菜单栏图标 → 退出）
# 或在终端：
pkill NBWindows
```

## 技术细节

- 纯 **Swift + SwiftUI** 原生开发
- 使用 **Accessibility API (AX)** 获取窗口状态
- 使用 **CGWindowList** 判断窗口可见性
- 无任何第三方依赖
- 支持 **Intel (x86_64)** 和 **Apple Silicon (arm64)**

## 隐私

- **完全本地运行**，不联网，不上传任何数据
- 源代码在 App 包内 `Contents/Resources/main.swift`，欢迎审查

## License

MIT

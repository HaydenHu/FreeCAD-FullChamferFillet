# FullChamfer & FullFillet - FreeCAD 完全倒角/圆角宏

两个 FreeCAD 宏，实现内置工具不支持的**完全倒角**和**完全圆角**功能。

## 背景

FreeCAD（基于 OpenCASCADE 内核）的 `PartDesign Chamfer` 和 `PartDesign Fillet` 不允许倒角距离/圆角半径等于或大于相邻面的最小边长，限制了"完全倒角/圆角"（倒角面完全覆盖原侧面）的实现。

本宏通过两种策略解决此问题：

- **半径 < 最小邻边长**：直接调用 FreeCAD 自带的 `PartDesign::Chamfer` / `PartDesign::Fillet`，创建标准参数化特征
- **半径 >= 最小邻边长**：构造自定义切割体（楔形/圆弧截面），通过布尔差集实现倒角/圆角

## 安装

### 方法一：手动安装

1. 下载本仓库所有文件
2. 将 `.FCMacro` 和 `.svg` 文件复制到 FreeCAD 宏目录：
   - Windows: `%APPDATA%\FreeCAD\Macro\`
   - Linux: `~/.local/share/FreeCAD/Macro/`
   - macOS: `~/Library/Preferences/FreeCAD/Macro/`

### 方法二：克隆仓库

```bash
cd <FreeCAD Macro 目录>
git clone https://github.com/HaydenHu/FreeCAD-FullChamferFillet.git .
```

## 添加到工具栏

1. 打开 FreeCAD，切换到 **PartDesign** 工作台
2. 菜单 **Tools → Customize**，切换到 **Macro** 标签页
3. 选中 `FullChamfer.FCMacro`：
   - 点击 `Pixmap` 旁的 `...`，选择 `FullChamfer.svg`
   - 设置 **Menu text** 为 `完全倒角`
   - 点击 `Add`，在弹窗的 **Workbenches** 中勾选 `PartDesign`
4. 同样操作 `FullFillet.FCMacro`：
   - Pixmap 选择 `FullFillet.svg`
   - Menu text 设为 `完全圆角`
5. 切换到 **Toolbars** 标签页，选择 `PartDesign`，将两个命令拖入工具栏
6. 点击 **Close**

## 使用方法
<img width="1280" height="688" alt="QQ20260517-191504" src="https://github.com/user-attachments/assets/f584fab2-bacf-4060-8759-7a09a73cf6df" />

1. 在 PartDesign 工作台中选中 Body 的一个 feature
2. 切换到边选择模式（点击工具栏的边选择图标）
3. 在 3D 视图中选中需要倒角/圆角的边（可多选）
4. 点击工具栏的 **完全倒角** 或 **完全圆角** 按钮
5. 在弹出的对话框中：
   - 输入**倒角距离**或**圆角半径**（默认值为完全覆盖所需值）
   - 对话框会提示当前将使用的方法（标准特征 / 布尔切割）
6. 确认执行

## 文件说明

| 文件 | 说明 |
|------|------|
| `FullChamfer.FCMacro` | 完全倒角宏 |
| `FullChamfer.svg` | 倒角图标 |
| `FullFillet.FCMacro` | 完全圆角宏 |
| `FullFillet.svg` | 圆角图标 |

## 兼容性

- FreeCAD 1.0+
- Part 和 PartDesign 工作台均支持
- Windows / Linux / macOS

## 许可

MIT License

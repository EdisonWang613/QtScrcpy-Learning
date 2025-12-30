# QtScrcpy-Learning (基于 C++ 与 Qt 的高性能投屏控制复现)

> **项目说明**：
> 本项目是基于开源项目 [QtScrcpy](https://github.com/barry-ran/QtScrcpy) 的深度学习与复现版本。
> 作为一个 C++ 后端研发方向的学习者，我通过拆解该项目，深入掌握了 **FFmpeg 音视频解码**、**OpenGL 渲染管线** 以及 **Socket 网络编程** 的核心实现原理。

---

## 👨‍💻 我的核心工作 (My Contributions)
*(注：这是我独立完成的学习与改进部分)*

### 1. 核心 Bug 修复与优化
*   **OpenGL 渲染色彩异常修复**：
    *   **问题**：在 Windows 新版显卡驱动环境下，发现旧版 OpenGL `GL_LUMINANCE` 格式兼容性失效，导致画面缺失红色通道（显示发青）。
    *   **解决**：重写渲染管线，将纹理格式迁移至现代标准的 `GL_RED`，并修改 Fragment Shader (片元着色器) 的采样算法，成功修复了色彩显示问题。
<table>
<tr>
    <td width="50%" align="center"><b>❌ 修复前 (Bug: 红色通道丢失)</b></td>
    <td width="50%" align="center"><b>✅ 修复后 (Normal: 色彩正常)</b></td>
</tr>
<tr>
    <!-- 注意：下面 src="" 引号里填你刚才复制的图片链接 -->
    <td><img src="https://github.com/user-attachments/assets/a929f445-6d21-497d-80e9-111e557ce1cc" width="100%"/></td>
    <td><img src="https://github.com/user-attachments/assets/14ff089c-0b68-4024-9433-09c6f973445f" width="100%"/></td>
</tr>
</table>

### 2. 环境构建与移植
*   **Windows 编译环境搭建**：
    *   独立配置了 MSVC 2019 + Qt 5.15 的编译环境。
    *   解决了 FFmpeg、SDL2 等第三方库在 Windows 平台下的动态链接依赖问题，编写了适配本地环境的 `CMakeLists.txt`。

### 3. 源码深度分析
*   **全流程注释**：对核心类（`Decoder` 视频解码、`YuvOpenGLWidget` 渲染、`Device` 设备管理）添加了详细的中文注释。
*   **原理梳理**：梳理了从 Socket 数据包接收 -> H.264 解码 -> YUV 数据上屏渲染的完整生命周期。

---

## ✨ 软件功能介绍 (Original Features)
*(注：以下是软件本身具备的强大功能，源自原项目架构)*

QtScrcpy 可以通过 USB (或通过 TCP/IP) 连接 Android 设备，并进行显示和控制。**不需要 root 权限**。

### 主要功能
*   **实时投屏**：低延迟（<80ms），高帧率（最高 60fps），高画质（1080P/2K）。
*   **反向控制**：使用电脑鼠标和键盘控制手机。
*   **按键映射**：支持自定义按键映射，可用于电脑玩手机游戏（吃鸡、王者荣耀等）。
*   **常用功能**：
    *   实时录屏（MP4格式）
    *   一键全屏显示
    *   无线连接（无需数据线）
    *   剪贴板同步（电脑手机复制粘贴互通）
    *   文件拖拽传输（直接拖文件进窗口即可发送到手机）

---

## 🏗️ 技术栈
*   **开发语言**: C++11
*   **GUI 框架**: Qt 5.15
*   **音视频处理**: FFmpeg (AVCodec Send/Receive 异步模型)
*   **图形渲染**: OpenGL ES (GLSL Shader)
*   **通信协议**: TCP Socket / ADB

---

## 📜 声明与版权 (Licence & Credits)

本项目仅供个人学习研究使用，在此特别鸣谢barry-ran同志。

*   **核心代码版权**：归原作者 **[barry-ran](https://github.com/barry-ran)** 所有。
*   **开源协议**：遵循 Apache License 2.0 协议。
*   **原项目地址**：https://github.com/barry-ran/QtScrcpy

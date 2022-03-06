# 编译 Fa 语言编译器

本文将简单描述如何在 Windows / macOS（未完成） / Linux（未完成） 环境下使用 Visual Studio / JetBrains Rider（未完成） 编译 Fa 语言编译器

## Windows 环境

### 使用 Visual Studio

1. 准备一台安装着 Visual Studio 的电脑
2. 克隆 fa 编译器仓库（`git clone https://github.com/fa-org/fa.git`）
3. 打开 `fa` 路径下的 `fa.sln`
4. 点击菜单 `Build` 下的 `Publish to Folder...`

> 接下来的步骤中，默认选择发布到的路径为默认（`bin/Release/net5.0/publish`），如果你更改了路径，到你设置的路径中寻找即可。

5. 前往 `fa` 路径下的 `fac/bin/Release/net5.0` 
6. 该路径下的 `fac` 或者 `fac.exe` 即为编译器

# GitHub仓库Fork更新最终版 Tool

[![COOLAPK](https://img.shields.io/badge/%E7%AD%B1%E7%AC%99%E5%A2%A8%E9%9C%B2-%E7%AD%B1%E7%AC%99%E5%A2%A8%E9%9C%B2?style=flat&logo=android&logoColor=FF4500&label=%E9%85%B7%E5%AE%89&color=FF4500
)](http://www.coolapk.com/u/20080253)
![Version](https://img.shields.io/badge/Version-2.0.0-brightgreen.svg)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20macOS%20%7C%20Windows%20%7C%20Android-blue.svg)
![Shell](https://img.shields.io/badge/Shell-Bash-yellow.svg)

一个强大的 GitHub 复刻仓库同步工具，可以自动将你的复刻仓库与上游原始仓库保持同步，确保你不会错过任何更新。

## 🌟 功能特性

- 🔄 **自动同步** - 一键同步复刻仓库的所有提交记录
- 🔐 **安全认证** - 使用 GitHub Token 进行安全认证
- 📱 **多平台支持** - 支持 Linux、macOS、Windows 和 Android (Termux)
- 🎯 **智能选择** - 自动列出所有复刻仓库供选择
- 🔄 **重试机制** - 网络操作失败时自动重试
- 💾 **配置保存** - Token 和配置信息安全保存
- 🛡️ **安全备份** - 自动备份本地更改

## 📋 前提条件

### 基础要求
- Git
- curl
- jq

### 各平台安装方法

#### Linux (Ubuntu/Debian)
```bash
sudo apt update && sudo apt install git curl jq
```

Linux (CentOS/RHEL/Fedora)

```bash
# CentOS/RHEL
sudo yum install git curl jq

# Fedora
sudo dnf install git curl jq
```

macOS

```bash
# 使用 Homebrew
brew install git curl jq
```

Windows

· 安装 Git for Windows
· 安装 jq for Windows

Android (Termux)

```bash
pkg update && pkg upgrade
pkg install git curl jq
```

🚀 快速开始

1. 获取脚本

```bash
# 克隆仓库
git clone https://github.com/2992253553/Github-fork-sync-tool.git
cd Github-fork-sync-tool

# 或者直接下载脚本
curl -O https://raw.githubusercontent.com/2992253553/Github-fork-sync-tool/main/github_fork_sync.sh
chmod +x github_fork_sync.sh
```

2. 运行脚本

```bash
./github_fork_sync.sh
```

3. 首次运行配置

首次运行时会要求进行 GitHub 认证：

1. 访问 GitHub Token 页面：
   · 打开 https://github.com/settings/tokens
   · 点击 "Generate new token"
   · 选择 "Generate new token (classic)"
2. 设置 Token 权限：
   · 备注：Fork Sync Tool
   · 勾选权限：
     · repo (全部仓库权限)
     · read:org (读取组织信息)
     · read:user (读取用户信息)
3. 生成并复制 Token：
   · 点击 "Generate token"
   · 复制生成的 Token 字符串
4. 在脚本中输入 Token：
   · 将复制的 Token 粘贴到脚本提示中
   · Token 会自动保存到安全位置

📖 详细使用教程

基本使用流程

1. 启动脚本：
   ```bash
   ./github_fork_sync.sh
   ```
2. 选择仓库：
   · 脚本会自动列出你的所有复刻仓库
   · 输入编号选择要同步的仓库
   · 显示每个仓库的最后更新时间
3. 自动同步：
   · 脚本会自动：
     · 克隆仓库（如果本地不存在）
     · 添加上游远程仓库
     · 获取所有最新提交
     · 重置本地分支到上游状态
     · 推送到你的复刻仓库
4. 查看结果：
   · 显示同步统计信息
   · 显示过去一年的提交数量
   · 显示最新提交信息

命令行选项

```bash
# 显示帮助信息
./github_fork_sync.sh --help

# 显示版本信息
./github_fork_sync.sh --version

# 清理配置和缓存
./github_fork_sync.sh --clean
```

Android (Termux) 专用教程

安装 Termux

1. 从 F-Droid 安装 Termux（推荐）
2. 或者从 GitHub Releases 下载最新版本

在 Termux 中设置

```bash
# 更新包管理器
pkg update && pkg upgrade

# 安装依赖
pkg install git curl jq

# 配置 Git（重要！）
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub邮箱"

# 获取脚本
cd ~
git clone https://github.com/2992253553/Github-fork-sync-tool.git
cd Github-fork-sync-tool
chmod +x github_fork_sync.sh

# 运行脚本
./github_fork_sync.sh
```

设置别名（可选）

```bash
# 编辑 bash 配置
nano ~/.bashrc

# 添加别名
alias sync-fork='~/Github-fork-sync-tool/github_fork_sync.sh'

# 重新加载配置
source ~/.bashrc

# 现在可以直接使用
sync-fork
```

🔧 高级配置

设置定期同步

使用 cron (Linux/macOS)

```bash
# 编辑定时任务
crontab -e

# 添加每周同步（每周日晚上10点）
0 22 * * 0 /path/to/github_fork_sync.sh

# 或者每天同步（凌晨2点）
0 2 * * * /path/to/github_fork_sync.sh
```

🛠️ 故障排除

常见问题

1. 认证失败

症状：Authentication failed 或 Invalid username or token

解决方案：

· 检查 Token 是否有效
· 重新生成 Token：https://github.com/settings/tokens
· 清理旧配置：./github_fork_sync.sh --clean

2. Git 安全目录错误

症状：detected dubious ownership in repository

解决方案：

```bash
# 修复 Git 安全目录
git config --global --add safe.directory /current/path
```

3. 网络连接失败

症状：fetch upstream failed 或网络超时

解决方案：

· 检查网络连接
· 设置代理（如果需要）：
  ```bash
  export https_proxy="http://proxy-ip:port"
  ```

📁 文件结构

```
Github-fork-sync-tool/
├── github_fork_sync.sh          # 主脚本文件
├── README.md                    # 说明文档
└── LICENSE                      # 许可证文件
```

配置文件位置

· Token 文件: ~/.github_fork_sync/token
· 配置缓存: ~/.github_fork_sync/repos_cache
· Git 凭证: ~/.git-credentials

🔒 安全说明

· 🔐 Token 安全：Token 以 600 权限保存在用户目录
· 🗑️ 清理凭证：使用 --clean 选项清理所有敏感信息
· 🔄 定期更新：建议定期更新 GitHub Token
· 📜 权限最小化：Token 只请求必要权限

🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支：git checkout -b feature/AmazingFeature
3. 提交更改：git commit -m 'Add some AmazingFeature'
4. 推送到分支：git push origin feature/AmazingFeature
5. 提交 Pull Request

📄 许可证

本项目采用 MIT 许可证 - 查看 LICENSE 文件了解详情

🙏 致谢

感谢以下项目的启发：

· GitHub CLI
· gh

📞 支持

如果你遇到问题：

1. 查看故障排除部分
2. 检查 Issues 是否有类似问题
3. 创建新的 Issue 并提供：
   · 操作系统和环境信息
   · 详细的错误信息
   · 复现步骤

---

Happy Syncing! 🚀

如果这个工具对你有帮助，请给个 ⭐ Star 支持一下！

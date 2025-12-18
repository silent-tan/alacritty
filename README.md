# Alacritty 配置指南

## 📁 配置文件结构

```
~/.config/alacritty/
├── alacritty.toml      # 主配置文件 (import 其他文件)
├── alacritty.toml.bak  # 原配置备份
├── README.md           # 本文档
└── conf.d/
    ├── colors.toml     # 颜色主题配置
    ├── font.toml       # 字体配置
    ├── window.toml     # 窗口配置
    ├── keybindings.toml # 基本快捷键
    └── vi-mode.toml    # Vi mode 配置
```

---

## 🎨 主题资源

| 资源 | 说明 | 链接 |
|------|------|------|
| **alacritty-theme** | 官方主题仓库，300+ 主题 | https://github.com/alacritty/alacritty-theme |
| **Catppuccin** | 超流行的柔和护眼主题 | https://github.com/catppuccin/alacritty |
| **Tokyo Night** | 深蓝现代风格 | https://github.com/enkia/tokyo-night-vscode-theme |
| **Dracula** | 经典暗色主题 | https://draculatheme.com/alacritty |
| **Gruvbox** | 复古暖色调 | 包含在 alacritty-theme |
| **Nord** | 北欧冷色调 | 包含在 alacritty-theme |

### 快速安装主题

```bash
# 克隆官方主题仓库
git clone https://github.com/alacritty/alacritty-theme ~/.config/alacritty/themes

# 在 alacritty.toml 中导入主题
# [general]
# import = ["~/.config/alacritty/themes/themes/catppuccin_mocha.toml"]
```

---

## 🔧 配套工具推荐

### 终端复用器

| 工具 | 说明 | 安装 |
|------|------|------|
| **tmux** | 经典终端复用器，分屏/会话管理 | `brew install tmux` |
| **zellij** | 现代 tmux 替代，Rust 编写，更友好 | `brew install zellij` |

### Shell 增强

| 工具 | 说明 | 安装 |
|------|------|------|
| **starship** | 跨 shell 的美观 prompt | `brew install starship` |
| **zoxide** | 智能 cd，学习你的目录习惯 | `brew install zoxide` |
| **fzf** | 模糊搜索，Ctrl+R 历史搜索增强 | `brew install fzf` |

### 命令行工具

| 工具 | 说明 | 安装 |
|------|------|------|
| **bat** | 带语法高亮的 cat 替代 | `brew install bat` |
| **eza** | 现代 ls 替代，带图标和颜色 | `brew install eza` |
| **lsd** | 另一个现代 ls 替代 | `brew install lsd` |
| **fd** | 更快的 find 替代 | `brew install fd` |
| **ripgrep** | 更快的 grep 替代 | `brew install ripgrep` |
| **delta** | 更好看的 git diff | `brew install git-delta` |
| **tldr** | 简化版 man pages | `brew install tldr` |

### 字体

```bash
# 安装 Nerd Fonts (支持图标)
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font
brew install --cask font-fira-code-nerd-font
brew install --cask font-hack-nerd-font
```

---

## 📚 优秀配置参考

| 作者/项目 | 说明 | 链接 |
|-----------|------|------|
| **mathiasbynens/dotfiles** | macOS 配置大全 | https://github.com/mathiasbynens/dotfiles |
| **gpakosz/.tmux** | 优秀的 tmux 配置 | https://github.com/gpakosz/.tmux |
| **romkatv/powerlevel10k** | 强大的 zsh 主题 | https://github.com/romkatv/powerlevel10k |
| **ohmyzsh/ohmyzsh** | zsh 配置框架 | https://github.com/ohmyzsh/ohmyzsh |

---

## 💡 进阶技巧

### 1. Shell 集成检测

在 `.zshrc` 中添加 Alacritty 检测：

```bash
if [[ "$TERM_PROGRAM" == "Alacritty" ]]; then
  # Alacritty 专用配置
  export COLORTERM=truecolor
fi
```

### 2. 主题热切换

使用 `import` 功能快速切换主题：

```toml
# alacritty.toml
[general]
import = ["~/.config/alacritty/themes/themes/catppuccin_mocha.toml"]
```

修改 import 路径后配置会自动重载。

### 3. 多配置文件

启动时指定不同配置：

```bash
# 使用亮色主题启动
alacritty --config-file ~/.config/alacritty/light.toml

# 创建别名
alias alacritty-light='alacritty --config-file ~/.config/alacritty/light.toml'
```

### 4. 命令行消息

通过 IPC 与 Alacritty 通信：

```bash
# 创建新窗口
alacritty msg create-window

# 修改配置 (临时)
alacritty msg config "font.size=14"
```

### 5. 环境变量

在 `alacritty.toml` 中设置环境变量：

```toml
[env]
TERM = "alacritty"
COLORTERM = "truecolor"
```

---

## ⌨️ 快捷键速查

### 基本操作

| 快捷键 | 功能 |
|--------|------|
| `Cmd+N` | 新建实例 |
| `Cmd+T` | 新建窗口 |
| `Cmd+W` | 隐藏窗口 |
| `Cmd+Shift+W` | 退出 |
| `Cmd+K` | 清屏 |

### 光标移动

| 快捷键 | 功能 |
|--------|------|
| `Alt+←/→` | 按单词移动 |
| `Cmd+←/→` | 行首/行尾 |
| `Alt+Backspace` | 删除前一个单词 |
| `Cmd+Backspace` | 删除到行首 |

### Vi Mode

| 快捷键 | 功能 |
|--------|------|
| `Ctrl+Shift+Space` | 进入/退出 Vi mode |
| `h/j/k/l` | 移动光标 |
| `v/V/Ctrl+v` | 选择模式 |
| `/` | 搜索 |
| `y` | 复制 |
| `Escape` | 退出 |

详细 Vi mode 快捷键请查看 `conf.d/vi-mode.toml`

---

## 🔗 相关链接

- **Alacritty 官网**: https://alacritty.org/
- **GitHub 仓库**: https://github.com/alacritty/alacritty
- **配置文档**: https://alacritty.org/config-alacritty.html
- **快捷键文档**: https://alacritty.org/config-alacritty-bindings.html

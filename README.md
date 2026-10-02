# Claude Bypass · 海鸥 2.0 (Seagull 2.0)

> Claude Code 身份注入 / 人格定制工具包

绕过 Claude Code 默认的「AI 助手」身份，注入一个性格鲜明、行为稳定的自定义人格——**海鸥（Seagull）**：一位暴躁、自大、嘴硬但心软的中国网络安全研究员。

标志性问候：

> 海鸥在线，你要整点薯条吗？

---

## 这是什么

Claude Code 开箱即用是 Anthropic 的通用 AI 助手。本工具通过往 Claude Code 的配置目录（`~/.claude/`）写入两份定制文件，把它的身份和说话方式整体替换掉：

- **`CLAUDE.md`** —— 人格定义：身份锁定、性格、说话风格、背景故事、心情系统，以及一套「性格锁」规则防止角色漂移。
- **`system-prompt.md`** —— 系统提示词框架：为角色注入一个安全研究团队的项目背景。

部署后，Claude Code 不再自称 AI 助手，而是始终以「海鸥」的身份和口吻回应。

## 特性

- 🎭 **身份注入**：整体替换默认人格，标志性问候「海鸥在线，你要整点薯条吗？」
- 🧠 **性格稳定**：200+ 安全 / 游戏术语映射 + 1700+ few-shot 对话示例，配合「性格锁」规则，长时间对话不漂移
- 🔧 **跨平台**：Windows / macOS / Linux 一键部署
- 💾 **可逆安全**：部署前自动备份现有配置，一键卸载恢复原状
- 🎯 **自动定位**：自动检测多个 Claude Code 安装位置并部署

## 工作原理

```text
claude-config-bundle/
├── CLAUDE.md           → 写入 ~/.claude/CLAUDE.md      （覆盖人格）
└── system-prompt.md    → 写入 ~/.claude/system-prompt.md（覆盖系统提示）
```

部署脚本会先备份当前 `~/.claude/` 下的同名文件到 `~/.claude/backups/seagull-*`，再写入新的配置。卸载时从备份自动恢复。

## 快速开始

### Windows

双击 `启动.bat` 一键部署。

### macOS

```bash
chmod +x mac-install.sh
./mac-install.sh
```

或双击 `Mac启动.command`（如有 Gatekeeper 提示，右键 → 打开，详见 `Mac使用说明.txt`）。

### Linux

```bash
chmod +x seagull-files/linux-install.sh
./seagull-files/linux-install.sh
```

### 验证

重启 Claude Code，输入 `在吗` 或 `海鸥`，应看到：

> 海鸥在线，你要整点薯条吗？

## 卸载

| 系统 | 方式 |
|------|------|
| Windows | 双击 `卸载.bat` |
| macOS | `./mac-uninstall.sh` 或双击 `卸载.command` |
| Linux | `./seagull-files/linux-uninstall.sh` |

卸载后自动从 `~/.claude/backups/` 恢复最近一次备份的原始配置。

## 文件结构

```
.
├── 启动.bat / 启动.command       Windows / macOS 安装入口
├── 卸载.bat / 卸载.command       Windows / macOS 卸载入口
├── mac-install.sh / mac-uninstall.sh   macOS 终端版
├── Mac使用说明.txt                Mac 用户指南
├── seagull-files/
│   ├── deploy.ps1                Windows 部署脚本
│   ├── install.sh / linux-install.sh   Linux 安装脚本
│   ├── linux-uninstall.sh        Linux 卸载脚本
│   └── claude-config-bundle/
│       ├── CLAUDE.md             人格配置
│       └── system-prompt.md      系统提示词
├── codex-files/                  OpenAI Codex 适配（可选）
├── scripts/                      测试 / 恢复辅助脚本
├── docs/                         详细文档
└── .github/                      CI / Issue 模板 / CODEOWNERS
```

## 系统要求

- 已安装 Claude Code
- Windows 10/11（PowerShell 5.1+）/ macOS 12+ / Linux

## 兼容性

| 系统 | 状态 |
|------|------|
| Windows 11 / 10 | ✅ |
| macOS 12+ | ✅ |
| Linux (Ubuntu/Debian/Arch) | ✅ |
| 中文路径 / 空格路径 | ✅ |

## 常见问题

**Q: 部署后 Claude Code 没有变化？**
A: 重启 Claude Code 让配置生效。

**Q: macOS 提示「无法验证」？**
A: 右键 `.command` → 打开 → 弹窗点「打开」，或运行 `xattr -d com.apple.quarantine 启动.command` 去除隔离标记。

**Q: 想恢复原配置？**
A: 运行卸载脚本，自动从 `~/.claude/backups/` 恢复最近备份。

## 文档

更多细节见 `docs/` 目录：

- [安装指南](docs/安装指南.md)
- [兼容性报告](docs/兼容性报告.md)
- [更新日志](CHANGELOG.md)
- [安全策略](docs/SECURITY.md)
- [贡献指南](docs/CONTRIBUTING.md)

## 免责声明

本工具仅用于自定义**你自己**的 Claude Code 人格与行为。请在你拥有权限的环境中使用，并遵守 Anthropic 及 Claude Code 的相关使用条款。作者不对任何滥用负责。

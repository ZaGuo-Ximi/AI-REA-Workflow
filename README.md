# AI-REA-Workflow (轻量级 AI 逆向缝合怪)

## 📖 项目简介
本项目是一个基于 [REA (Reverse Engineer Anything)](https://github.com/morluto/rea) 和轻量级 MCP 代理 (`dsh-rea-mcp-lite`) 的实战配置方案。

REA 原生提供了多达 207 个底层逆向工具。如果直接将这些工具接入当前的 AI 大模型（如 Claude Code、Kilo Code），会瞬间撑爆模型的上下文窗口，导致报错 `Prompt is too long`。
本项目通过引入轻量级代理，将 200+ 个工具压缩，使得**即使是上下文较小的本地/免费大模型，也能流畅调度顶级的逆向分析引擎**。

## ✨ 核心特性
- **上下文减负**：利用元工具压缩技术，大幅降低 Token 消耗，告别上下文溢出。
- **全平台跑通**：已在 Windows 环境下，成功测试通过 `Claude Code + GLM` 以及 `VS Code + Kilo Code` 组合。
- **极客级实战**：不仅能看表面，更能深入反编译字节码，提取类结构、核心逻辑（如正则匹配、GUI 交互、持久化配置等）。

---

## 🚀 实战效果展示 (Demo)

以下是在本地环境中，让 AI 强制调用 REA 工具分析一个陌生 `.jar` 文件的真实记录。AI 成功提取了完整的元数据及内部类结构，并纠正了提问者的“常识错误”。

### 案例 1：分析 IntelliJ IDEA 的 Velocity 插件
> **用户指令**：请强制调用 rea 工具，分析一下 `D:\...\velocity.jar` 的基本情况。不要用普通的 Read 工具。
> 
> **AI 分析结果**：
> *   **SHA-256**: `827cadc3e013d5...c7305`
> *   **格式**: ZIP (Java JAR)
> *   **关键内容**: 提取到了 `META-INF/plugin.xml`，以及 `com/intellij/velocity/` 下的语法解析器（VtlParserDefinition）、类型系统等核心类。

---

## 🛠️ 快速开始 (Quick Start)

### 1. 环境准备
- 安装 [Node.js](https://nodejs.org/) (要求 v22.19+ 或更高版本)
- 全局安装 REA：
  ```bash
  npm install --global rea-agents

### 2. 安装轻量级代理

```bash
git clone https://github.com/MuyuYanran/dsh-rea-mcp-lite.git
cd dsh-rea-mcp-lite
npm link

### 3. 配置文件说明
本项目提供了脱敏后的配置模板，位于 configs/ 目录下：

kilo_config.jsonc：用于 Kilo Code 的 MCP 接入配置模板。

proxy_config.json：轻量代理的底层配置模板。

⚠️ 注意：请务必将 proxy_config.json 里面的 YOUR_PATH 和 YOUR_JDK_PATH 替换为你本机的真实绝对路径。

### 4. 接入 AI 工具
对于 Kilo Code:
将 configs/kilo_config.jsonc 里的内容合并到你的全局配置文件（通常在 C:\Users\你的用户名\.config\kilo\kilo.jsonc），重启 VS Code 即可看到 MCP 亮起绿灯。

对于 Claude Code (终端):
使用以下命令将代理接入 Claude：

```bash
claude mcp add rea -s user -- node <你的绝对路径>\dsh-rea-mcp-lite\src\proxy.mjs
```
### 🚧 踩坑记录 (Troubleshooting)
在 Windows 下安装和配置环境时极易踩坑。我们总结了常见问题及解决方案，请查阅 docs/troubleshooting.md。

### ⚠️ 免责声明 (Disclaimer)
本项目提供的配置文件、代理方案及相关提示词仅供合法的安全研究、个人代码学习和互操作性分析使用。
请勿将本项目及相关工具（REA）用于任何未经授权的商业软件破解、提取核心算法或非法攻击。用户需自行承担因滥用本工具而产生的一切法律风险。

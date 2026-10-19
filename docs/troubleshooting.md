\# 常见问题与踩坑记录 (Troubleshooting)



在 Windows 环境下部署 REA 和轻量级代理时，你可能会遇到以下问题。这里是我们的实战解决记录。



\## 1. 安装 REA 时报错 `EBUSY: resource busy or locked`

\- \*\*原因\*\*：Windows 系统下文件被占用，或者 npm 缓存损坏。

\- \*\*解决\*\*：

&#x20; 1. 关闭所有命令行窗口。

&#x20; 2. 以\*\*管理员身份\*\*运行 CMD。

&#x20; 3. 执行 `npm cache clean --force`。

&#x20; 4. 如果依然报错，请直接重启电脑释放文件锁，然后重新执行 `npm install`。



\## 2. Claude Code / Kilo 报错 `Prompt is too long`

\- \*\*原因\*\*：REA 原生 200 多个工具定义会瞬间塞满大模型的上下文窗口。

\- \*\*解决\*\*：必须使用本项目提供的 `dsh-rea-mcp-lite` 轻量级代理，将工具压缩为元工具。



\## 3. 模型“发疯”或胡乱回答（如强行写一段 Python 代码）

\- \*\*原因\*\*：使用的免费/轻量级模型（如 GLM-4-Flash）工具调用（Function Calling）能力极差，容易被复杂指令误导。

\- \*\*解决\*\*：

&#x20; 1. 换用更聪明的模型（如 GPT-4o、Claude 3.5 Sonnet，或国内强力的 DeepSeek、GLM-4-Plus）。

&#x20; 2. 使用项目 `prompts/reverse\_engineer.md` 中的“强指令”，逼迫模型去调用工具。



\## 4. API 报错 `529 \[1305]` 或连接超时

\- \*\*原因\*\*：使用的第三方 API（如智谱）服务器过载，或网络波动。

\- \*\*解决\*\*：稍等几分钟重试，或者在配置中更换其他模型节点。


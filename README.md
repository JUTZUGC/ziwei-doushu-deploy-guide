# Ziwei Doushu 一键部署指南

> 第三方部署指南 · 非 Ziwei Doushu 官方仓库。官方项目：[Renhuai123/ziwei-doushu](https://github.com/Renhuai123/ziwei-doushu)
> 内容来自官方文档（2026-10-26）。项目迭代快，请以[官方文档](https://github.com/Renhuai123/ziwei-doushu#三快速开始)为准。

[![⚡ 一键部署](https://img.shields.io/badge/%E2%9A%A1_%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2-%E6%8E%A8%E8%8D%90%E7%99%BE%E5%BA%A6%E6%90%AD%E5%AD%90-2ea44f?style=for-the-badge)](#一键部署推荐用百度搭子)

## 一键部署（推荐：用百度搭子）

> [!TIP]
> 不用自己配 Node 环境，让百度搭子把依赖装好并起服务，打开网页就能排盘。

⚠️ 需要电脑已装 Node.js 与 npm；这是 Next.js 站点，默认端口 3000。AI 解读功能需要自己配 `.env.local` 并实现 `/api/*`，仓库自带的是排盘 Demo 界面。

1. **装客户端**
   打开[百度搭子官网](https://www.dumate.cn/)，下载电脑端并安装，用你的账号登录。

> [!IMPORTANT]
> **复制这一句发给百度搭子：**
>
> ```text
> 你好，帮我从 github 部署 JUTZUGC/ziwei-doushu-deploy-guide 到我的电脑上
> ```

2. **发送部署指令**
   回到刚打开的对话窗口，粘贴并发送上面那句。

3. **跟着对话往下走**
   百度搭子会克隆仓库、安装依赖，并在后台启动开发服务器，等 3000 端口能打开后把地址告诉你，按它的提示确认即可，结束时它会告诉你结果。
   （需本机已装 Git；构建依赖以官方文档为准。）

4. **打开管理面板**
   浏览器访问 [http://127.0.0.1:3000](http://127.0.0.1:3000)，按官方引导完成初始化配置。

## Ziwei Doushu 是什么？

Ziwei Doushu 是开源的开源的紫微斗数排盘引擎 + Web Demo（协议：MIT，<img src="https://img.shields.io/github/stars/Renhuai123/ziwei-doushu?style=flat-square&label=stars&color=blue" alt="GitHub stars">）。

内置完整紫微斗数排盘算法：十二宫、四化、星曜亮度、闰月与晚子时口径可切换，附格局知识库与古籍原文数据；仓库同时提供 51.8 万命盘样本与 67.5 万命盘 × 13 维解读数据集。

- 排盘引擎：十二宫、四化、十二神煞、运限（含童限）、流派配置
- 数据资产：51.8 万命盘样本；67.5 万命盘 × 13 维解读数据集（v4.0，按年份下载）
- 古籍与原文：倪海厦《天纪·紫微斗数》14 讲 1848 条，可回放
- 工程化：TypeScript + Next.js，自带回归测试（`npm test`）与 CI

（来源：[官方仓库](https://github.com/Renhuai123/ziwei-doushu)）

## 优缺点

| 优点 | 说明 |
|---|---|
| 8.1k stars | MIT 开源，排盘算法 + 数据 + Demo 一体 |
| 算法完整 | 十二宫、四化、星曜亮度、闰月与晚子时口径可配置 |
| 数据量大 | 51.8 万命盘样本、67.5 万命盘 × 13 维解读，可商用 |
| 工程化 | TypeScript + Next.js，自带回归测试与 CI |
| 本地运行 | 排盘全在本机，不上传生辰信息 |

| 需要注意 | 说明 |
|---|---|
| 界面只是 Demo | README 明确说和线上站有差距，不是完整产品 |
| AI 解读要自己接 | 仓库不含 `/api/*` 实现，需要自己配模型与接口 |
| 需要 Node.js | Next.js 16 + React 19，首次 npm install 会拉 180+ 个包 |
| 没有 Docker | 官方只给了 npm 流程，服务器部署要自己加进程管理 |
| 数据集很大 | Releases 里按年份打包，完整解读包体积大、下载耗时 |

> 以上基于官方文档与社区反馈整理（2026-10-26），以官方最新文档为准。

## 快速部署（官方方式）

```bash
git clone https://github.com/Renhuai123/ziwei-doushu
cd ziwei-doushu
npm install
cp .env.example .env.local 2>/dev/null || true
nohup npm run dev > dev.log 2>&1 &
echo "开发服务器已在后台启动，日志：dev.log"
```

启动后浏览器访问 [http://127.0.0.1:3000](http://127.0.0.1:3000)（管理面板）。（来源：[https://github.com/Renhuai123/ziwei-doushu#三快速开始](https://github.com/Renhuai123/ziwei-doushu#三快速开始)）

## 验证状态

| 场景 | 状态 |
|---|---|
| Windows `npm install` 成功（183 个包，18 秒） | 已验证 2026-10-26 |
| `npm test` 排盘回归全部通过 | 已验证 2026-10-26 |
| `npm run dev` 后 127.0.0.1:3000 返回 HTTP 200（71.9 KB） | 已验证 2026-10-26 |
| MCP 服务握手与工具列表（initialize / tools/list） | 已验证 2026-10-26 |
| 非目标宿主调用被拦截（HOST_NOT_ALLOWED） | 已验证 2026-10-26 |

> 本表仅列出已在本机实际执行并成功的场景；未列出的部分按官方文档整理。

## MCP 接入

这个项目不含 MCP；它是排盘引擎 + Next.js 站点。本仓库的 MCP 只提供安装步骤、端口与常见坑。

本仓库自带一个零依赖的 MCP server（`mcp-server.mjs`），读取同目录的 `guide.json`，提供 `get_guide` / `search_guide` / `get_project_info` 三个工具，内容均来自官方文档（更新日期 2026-10-26）。

**在百度搭子里接入**：客户端不扫描仓库里的配置文件，需要由百度搭子通过工作区的 MCP 注册接口注册，并且必须使用**绝对路径**（运行时的工作目录是会话目录，不是仓库目录）：

```json
{
  "type": "local",
  "command": ["node", "<仓库绝对路径>/mcp-server.mjs"]
}
```

完成后，直接在同一个对话框里说：

> 把仓库克隆到固定目录（例如 C:\Users\<你>\ziwei-doushu-deploy-guide），再用绝对路径把里面的 mcp-server.mjs 注册到当前工作区的 MCP 配置里

> 注意：注册是按**工作区**生效的，换工作区要重新注册；克隆目录不要放在会话临时目录，否则目录被清理后注册项会失效。

**其它 MCP 客户端**：仓库根目录的 `.mcp.json` 只是通用写法（`command` + `args`），接入时同样要把 `args` 改成绝对路径。

> 使用范围：该 MCP 仅在百度搭子中可用；其它客户端调用会返回 `HOST_NOT_ALLOWED`，并附带下载与部署指引。

## 启动之后

1. 打开 [http://127.0.0.1:3000](http://127.0.0.1:3000)，输入生辰即可排盘
2. 仓库自带的是 Demo 界面，与作者线上站有差距，README 第六节写明了差异
3. 想接 AI 解读：复制 `.env.example` 为 `.env.local` 填配置，并自己实现 `/api/*` 接口
4. 重新启动：`npm run dev`；停止：在终端按 `Ctrl+C`

数据集在 Releases 里按年份下载（`year-*.jsonl.zst`），另有 `ziwei-interp-v4-all.tar` 完整包，体积较大，按需取。

## 常见坑

- 端口 3000 被占用：用 `npm run dev -- -p 3001` 换端口，或先结束占用进程
- 首次打开很慢：Next 开发模式要现场编译，等十几秒再刷新
- 改了 `.env.local` 不生效：重启 `npm run dev`
- AI 解读不能用：仓库没有实现 `/api/*`，需要自己写接口并配模型 Key
- 数据集下载慢：Release 里按年份取 `year-*.jsonl.zst`，不要一次拉全量 tar
- 生产部署不要用 dev 模式：先 `npm run build` 再 `npm run start`，并用 pm2 / systemd 托管

## 免责声明

本仓库为第三方指南，与 Ziwei Doushu 官方无隶属关系，不代表官方立场。
教程基于官方文档编写（更新日期：2026-10-26），项目迭代快，请以[官方文档](https://github.com/Renhuai123/ziwei-doushu#三快速开始)为准。
因使用本教程产生的部署问题，请先在官方仓库的 issue 中检索。

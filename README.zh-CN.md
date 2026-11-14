# Nextrap Skills

[English](README.md) | **简体中文**

用于 Nextrap CLI 的 Agent Skill，帮助 AI 从 IP、URL 或产品名称调查公共攻击情报，选择所需查询，并把日志、统计和前后请求组织成可复核的答案。

支持日志字段与检索、全文与单条解密、相邻请求、去重计数、请求分布、IP 归属与活动，以及认证、余额查询和 CLI 自更新。

## 安装

```bash
npx skills add nextrap-net/nextrap-skills --skill nextrap-cli
```

按提示选择 AI 工具。需要全局安装时使用：

```bash
npx skills add nextrap-net/nextrap-skills --skill nextrap-cli -g
```

安装技能不会安装 CLI 程序。请单独准备 `nextrap-cli`，加入 PATH 或向 AI 提供它的可执行文件路径。

## 使用前

确认 CLI 可用，并通过标准输入保存 API Key：

```bash
nextrap-cli --version
nextrap-cli auth set --api-key -
nextrap-cli status
```

API Key 在 Nextrap 平台个人中心创建。在本机终端向认证命令提供标准输入；不要把 Key 发到聊天、写进命令参数或提交到仓库。`status` 用于查看当前身份与情报余额。

## 可以这样提问

将以下地址、日期和名称替换为实际线索：

- **IP**：“调查 `203.0.113.10` 在 2026-11-13 至 2026-11-14 的活动，取三条请求；必要时看其中一条此前的动作，不要解密。”
- **URL**：“查看 `/api/auth/login` 相关请求，说明主要来源和请求特征，保留能复核的日志定位信息。”
- **产品**：“查看名称包含 `WordPress` 的产品在指定日期收到什么请求，统计不同来源 IP 数，并说明名称匹配范围。”

Skill 会按问题选择样例、活动、计数或分布；需要继续时，再从真实结果取得单条定位信息。已有日志 ID、日期和产品编号时，可以直接提供，减少重复查询。

## 结果与边界

- 按需查询，不自动翻页、扩大日期或批量解密。查询和解密可能消费额度，权限与实际消费由平台判断。
- 单条操作使用同一记录的 ID、真实日期和产品编号；不从产品名称猜编号，不混用不同记录的定位值。
- 区分请求数、不同对象数、分布桶数和样例条数；保留桶标签及计数，并解释近似、打码、截断和未知字段。
- 观测到请求不等于攻击成功，空结果不等于目标安全；不据此确认漏洞或攻击者身份。

## 技能结构

```text
skills/
└── nextrap-cli/
    ├── SKILL.md
    └── references/
```

## 文档

- [Skill 入口与命令路由](skills/nextrap-cli/SKILL.md)
- [从来源 IP 调查公共请求](skills/nextrap-cli/references/workflow-ip-investigation.md)
- [从 URL 或产品名称调查请求](skills/nextrap-cli/references/workflow-url-product-investigation.md)
- [从请求分布定位日志样例](skills/nextrap-cli/references/workflow-distribution-drilldown.md)

## 发布版本

[v1.0.0](https://github.com/nextrap-net/nextrap-skills/releases/tag/v1.0.0) 是技能的初始版本。技能与 CLI 程序分别分发。

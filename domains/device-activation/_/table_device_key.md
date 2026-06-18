---
id: tbl_device_key
object_type: Table
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- 设备
- 公钥
subdomain: null
module: null
sensitivity: normal
name: 设备公钥表
aliases:
- t_device_key
related_services: []
related_tables:
- tbl_hardware_info
related_scenarios:
- flow_device_activation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储设备公钥信息。设备首次激活后，与设备硬件信息一同落库，用于后续设备身份校验/通信加密相关场景。

## 关键列
- `id`：与 `t_hardware_info.id` 关联（`t_device_key.id = t_hardware_info.id`）。

> 原文未列出更多字段，公钥具体列名未给出。

## 主键/索引
- `id` 与 `t_hardware_info.id` 一一对应（基于原文 `id=t_hardware_info.id` 的关联约定）。

## 校验点(QA 关注)
- 设备首次激活成功后，`t_device_key` 应有对应记录，且 `id` 与 `t_hardware_info.id` 一致。
- 校验 `t_device_key` 与 `t_hardware_info` 的关联完整性：不应出现 `t_hardware_info` 有记录而 `t_device_key` 缺失的情况。
- 查询命令：`select * from device.t_device_key;`

</details>

---

## File: scenarios/inspect-cards/scenario_inspect_cards.md

# AI 提示词与上下文（来自 build-card 流水线）

> 模型: claude-haiku-4-5 ｜ 模式: General

## System Prompt

<details><summary>展开查看</summary>

你是资深支付 QA，把文档里某个技术对象整理成结构化知识对象。先输出元数据 JSON，再输出正文 markdown——正文绝不放进 JSON(避免转义/截断)。

</details>

## User Prompt

<details><summary>展开查看</summary>

根据【整篇原文】，把对象 id=scenario_inspect_cards (Scenario, name=AI 上下文检查（inspect-cards）) 整理出来。

第一部分：输出元数据 JSON(单行紧凑，**不含正文**)：
{"id":"scenario_inspect_cards","object_type":"Scenario","domain":"build-card","name":"AI 上下文检查（inspect-cards）",
"aliases":["inspect cards","prompt 审计"],"tags":["调试","AI 提示词","审计"],"subdomain":null,"module":null,
"related_services":["service_build_card"],"related_tables":[],"related_scenarios":["scenario_object_extraction"],"related_logs":[],"related_failures":[]}
(subdomain/module 可选，无合适值留 null；related_* 用真实 id，无则留空数组——优先取自【可链接清单】)

第二部分：单独一行写 `===BODY===`，然后输出正文 markdown，按此骨架：
## 场景目标
## 触发命令 / 入口
## 前置条件
## 处理流程
## 产出
## 用途与限制

正文要求：忠实且精炼；只写本对象 scope=审计某个对象正在使用的 AI 提示词与上下文 的内容。

【可链接清单】
- [[build-card-overview]] build-card 流水线概览
- [[service_build_card]] (Service) build-card CLI 服务
- [[scenario_object_extraction]] (Scenario) 单个对象抽取
- [[tbl_objects_yaml]] (Storage) objects.yaml

【整篇原文】
build-card CLI 提供一个调试用子命令 `inspect-cards`，用于审计某个对象在生成时实际收到的 system / user prompt。

## 命令格式

```
build-card inspect-cards --id <object-id>
```

例如：

```
build-card inspect-cards --id tbl_device_key
```

## 行为

1. 读取 `objects.yaml`，定位目标对象。
2. 重新构造 system prompt 和 user prompt（与正常 build 时一致），但不调用 LLM。
3. 把 prompt 内容输出到 `scenarios/inspect-cards/scenario_<id>.md`。

输出文件包含：

- 模型 ID（例如 claude-haiku-4-5）
- 系统提示词
- 用户提示词（包括【可链接清单】和【整篇原文】节选）

## 用途

- 排查“为什么这个对象抽取出来字段不对” → 看 user prompt 是否包含正确的原文段落。
- 评审 prompt 工程改动 → 在不消耗 LLM 调用的情况下 diff prompt 文本。
- 复现历史问题 → 把 inspect 输出贴给同事或 LLM 复盘。

## 限制

- inspect-cards 只反映“当前 objects.yaml + 当前代码”的 prompt 状态；如果 prompt 模板更新了，老卡片对应的真实历史 prompt 不会被保留。
- 不会触发实际 LLM 调用，因此不会更新卡片正文，仅供审计。


</details>

---

## File: scenarios/object-extraction/scenario_object_extraction.md

# AI 提示词与上下文（来自 build-card 流水线）

> 模型: claude-haiku-4-5 ｜ 模式: General

## System Prompt

<details><summary>展开查看</summary>

你是资深支付 QA，把文档里某个技术对象整理成结构化知识对象。先输出元数据 JSON，再输出正文 markdown——正文绝不放进 JSON(避免转义/截断)。

</details>

## User Prompt

<details><summary>展开查看</summary>

根据【整篇原文】，把对象 id=scenario_object_extraction (Scenario, name=单个对象抽取) 整理出来。

第一部分：输出元数据 JSON(单行紧凑，**不含正文**)：
{"id":"scenario_object_extraction","object_type":"Scenario","domain":"build-card","name":"单个对象抽取",
"aliases":["object extraction"],"tags":["AI","抽取","卡片"],"subdomain":null,"module":null,
"related_services":["service_build_card"],"related_tables":[],"related_scenarios":["scenario_inspect_cards"],"related_logs":[],"related_failures":[]}
(subdomain/module 可选，无合适值留 null；related_* 用真实 id，无则留空数组——优先取自【可链接清单】)

第二部分：单独一行写 `===BODY===`，然后输出正文 markdown，按此骨架：
## 场景目标
## 输入 / 上下文
## 处理流程
## 产出与落盘
## 校验与回退

正文要求：忠实且精炼；只写本对象 scope=用 LLM 把单个 object 抽取为卡片正文 + 元信息 的内容。

【可链接清单】
- [[build-card-overview]] build-card 流水线概览
- [[service_build_card]] (Service) build-card CLI 服务
- [[scenario_inspect_cards]] (Scenario) AI 上下文检查
- [[tbl_objects_yaml]] (Storage) objects.yaml

【整篇原文】
单个对象抽取（object extraction）是 build-card 流水线的核心处理步骤。它把一段“整篇原文 + 一个 object 定义”交给

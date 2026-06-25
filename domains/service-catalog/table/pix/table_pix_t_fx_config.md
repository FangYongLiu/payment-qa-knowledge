---
id: tbl_pix_t_fx_config
object_type: Table
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:3ba2b4cb-ed33-4ef7-b5cb-0b2b6210e1e9
tags:
- pix
- fx
- config
subdomain: pix
module: fx-rate
sensitivity: normal
name: PIX FX配置表 t_fx_config
aliases:
- pix.t_fx_config
- FX Config
related_services:
- svc_pix
---

## 用途
PIX 渠道 FX 配置表，按 `channel_code` + `currency_code` 维度存储 FX 汇率上下限与启用标志，并通过 `rate_version_id` / `margin_version_id` 分别引用 [[tbl_pix_t_fx_rate_version]] 与 [[tbl_pix_t_fx_margin_version]] 中的版本化汇率与 Margin 记录，实现版本化的 FX 汇率/Margin 管理。

## 关键列
| 列名 | 类型 | 说明 |
|---|---|---|
| channel_code | varchar(32) | 渠道编码，主键 |
| currency_code | char(3) | 币种编码 |
| min_rate | decimal(15,8) | 汇率下限 |
| max_rate | decimal(15,8) | 汇率上限 |
| rate_version_id | bigint | 引用 `t_fx_rate_version.version_id` |
| margin_version_id | bigint | 引用 `t_fx_margin_version.version_id` |
| enable_flag | char(1) | 启用标志 |

## 主键/索引
- 主键：`channel_code`
- 外键关系（ER 图所示）：
  - `rate_version_id` → `t_fx_rate_version.version_id`
  - `margin_version_id` → `t_fx_margin_version.version_id`

## 校验点(QA 关注)
- `min_rate` / `max_rate` 的精度为 decimal(15,8)，应校验上下限非空且 `min_rate ≤ max_rate`。
- `rate_version_id`、`margin_version_id` 必须能在对应版本表中找到匹配 `version_id`，且版本表中的 `channel_code` / `currency_code` 应与本表一致。
- `enable_flag` 控制该 (channel_code, currency_code) 组合是否生效，停用时相关 FX 流程应跳过或拒绝。
- 切换汇率/Margin 版本时，应通过更新 `rate_version_id` / `margin_version_id` 指向新版本，而非修改历史版本记录，以保留版本化追溯。

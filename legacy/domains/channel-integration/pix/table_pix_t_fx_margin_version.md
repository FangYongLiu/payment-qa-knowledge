---
id: tbl_pix_t_fx_margin_version
object_type: Table
domain: channel-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:3ba2b4cb-ed33-4ef7-b5cb-0b2b6210e1e9
tags:
- pix
- fx
- margin
- versioned
subdomain: pix
module: fx-rate
sensitivity: normal
name: PIX FX Margin版本表 t_fx_margin_version
aliases:
- pix.t_fx_margin_version
- FX Margin Version
related_services: []
related_tables:
- tbl_pix_t_fx_config
- tbl_pix_t_fx_rate_version
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储 PIX 渠道按 channel_code + currency_code 维度的汇率 Margin 百分比的版本化记录。被 `t_fx_config.margin_version_id` 通过外键引用，实现 FX Margin 的可版本化管理(支持历史版本追溯/切换)。

## 关键列
- `version_id` (bigint, PK)：Margin 版本号，作为主键，被 `pix.t_fx_config.margin_version_id` 引用。
- `channel_code` (varchar)：渠道编码。
- `currency_code` (char(3))：币种编码。
- `rate_margin_percent` (decimal(_,8))：汇率 Margin 百分比，精度小数 8 位。
- `operator` (varchar)：操作人。

## 主键/索引
- 主键：`version_id`。
- 外键关系(被引用)：`pix.t_fx_config.margin_version_id` → `pix.t_fx_margin_version.version_id`。

## 校验点(QA 关注)
- `version_id` 必须唯一且被 `t_fx_config.margin_version_id` 正确引用，确保 Config 指向的 Margin 版本存在。
- 同一 `channel_code` + `currency_code` 组合应允许存在多版本记录，用于版本切换/回溯。
- `currency_code` 固定 char(3)，需符合 ISO 4217 三位币种码。
- `rate_margin_percent` 精度为小数 8 位，需校验入库精度无截断；业务上需校验是否在合法范围(避免负值或超大值)。
- `operator` 必须记录变更人，便于审计。
- 与 `t_fx_rate_version` 解耦：Margin 版本与 Rate 版本独立维护，QA 需验证两者各自切换互不影响 `t_fx_config` 的另一引用。

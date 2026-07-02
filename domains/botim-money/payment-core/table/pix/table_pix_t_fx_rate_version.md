---
id: tbl_pix_t_fx_rate_version
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:3ba2b4cb-ed33-4ef7-b5cb-0b2b6210e1e9
tags:
- pix
- fx
- versioned
subdomain: pix
module: fx-rate
sensitivity: normal
name: PIX FX汇率版本表 t_fx_rate_version
aliases:
- pix.t_fx_rate_version
- FX Rate Version
related_services:
- svc_pix
---

## 用途
位于 `pix` schema 下，存储按渠道+币种维度版本化的 FX 汇率记录。被 `t_fx_config.rate_version_id` 通过外键引用，从而实现汇率的版本化管理(可追溯历史汇率版本)。

## 关键列
- `version_id` bigint — 版本主键
- `channel_code` varchar(32) — 渠道代码
- `currency_code` char(3) — 币种代码
- `exchange_rate` decimal(15,8) — 汇率值
- `operator` varchar(50) — 操作人

## 主键/索引
- 主键：`version_id`
- 外键关系：被 `t_fx_config.rate_version_id` 引用至本表 `version_id`

## 校验点(QA 关注)
- `t_fx_config.rate_version_id` 必须能在本表中找到对应 `version_id`，否则配置指向悬空版本。
- `channel_code` + `currency_code` 应与引用方 `t_fx_config` 的同名字段保持一致(同一渠道/币种的版本归属)。
- `exchange_rate` 精度为 decimal(15,8)，校验值落在 `t_fx_config.min_rate` 与 `max_rate` 之间。
- 版本化语义：旧版本记录应保留(用于审计/回溯)，更新汇率应生成新 `version_id` 并更新 `t_fx_config.rate_version_id` 指向。
- `operator` 用于审计，应记录变更人。

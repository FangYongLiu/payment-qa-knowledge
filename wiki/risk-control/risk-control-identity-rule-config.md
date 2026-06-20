---
title: 风控核身规则配置说明
domain: risk-control
kind: wiki_page
slug: risk-control-identity-rule-config
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:177543ab-8600-454c-ad0f-81030f9f5112
tags: []
---

# 风控核身规则配置说明

本页说明风控核身规则在 Redis 中的缓存 Key 命名以及商户核身数据的存储结构示例，便于在配置/排查风控核身规则时定位对应缓存数据。

## Redis 连接与库

- 连接名：`Payby_Sim_Azure`
- 数据库：`DB0`

## 核身相关缓存 Key

在 `DB0` 中以前缀 `grc` 检索，可见以下两类 Key：

- `gp079_grc-check-identity-provider`（1 条）
  - 用途：核身校验（check identity）相关配置/数据
- `gp079_grc-component-connect-provider`（167 条）
  - 用途：核身组件连接（component connect）相关配置/数据

## 商户核身数据示例

以 Key `gp045_merchar...`（String 类型）为例：

- 类型：String
- TTL：`7249778`
- 大小：`3.98KB`
- 序列化格式：Json

JSON 内容（节选）字段示例：

- `paymen...`: `"601"`
- `taxRegCertificatePath`: `"20240920/1726837793478.png"`
- `taxRegistrationNo`: `"434645765235346"`
- `tradeLicenseNo`: `"43645325634"`
- `website`: `"www.payby.com"`
- `merchantMid`: `"200000432860"`

字段说明（按用途）：

- 商户标识：`merchantMid`
- 税务相关：`taxRegistrationNo`（税号）、`taxRegCertificatePath`（税务登记证文件路径）
- 营业执照：`tradeLicenseNo`
- 站点信息：`website`

## 使用提示

- 通过 `gp079_grc-*` 前缀可快速过滤出核身规则相关 Key。
- 商户维度的核身资料以 JSON 串形式缓存，包含税务、营业执照、站点等关键资质字段，可用于核身规则匹配与校验。

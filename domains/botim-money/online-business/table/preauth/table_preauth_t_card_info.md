---
id: tbl_preauth_t_card_info
object_type: Table
name: 支付卡信息 (t_card_info)
aliases: [t_card_info, preauth.t_card_info]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: preauth schema DDL
tags: [online-business, preauth]
sensitivity: normal
related_services: []
---

# 支付卡信息 (t_card_info)

## 用途
物理表 `preauth.t_card_info`,主键 `global_id`。支付卡信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `brand` | varchar(32) | 卡组织 · 可空 |
| `card_id` | varchar(32) | 卡ID · 可空 |
| `card_num` | varchar(32) | 卡号 · 可空 |
| `holder_name` | varchar(32) | 持卡人 · 可空 |
| `exp_year` | varchar(32) | 过期年份 · 可空 |
| `exp_month` | varchar(32) | 过期月份 · 可空 |
| `card_type` | varchar(32) | 卡类型 · 可空 |
| `card_expired_ues_token` | varchar(32) | cardExpired · 可空 |
| `card_num_maskii` | varchar(32) | cardNumMask2 · 可空 |
| `card_num_mask` | varchar(32) | 卡号掩码 · 可空 |
| `card_token` | varchar(64) | cardToken · 可空 |
| `access_type` | varchar(32) | 访问类型 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `card_token_exp_time` | timestamp(3) | cardToken过期时间 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

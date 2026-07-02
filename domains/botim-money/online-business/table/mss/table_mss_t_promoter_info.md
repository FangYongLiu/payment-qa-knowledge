---
id: tbl_mss_t_promoter_info
object_type: Table
name: 商户推广员信息表 (t_promoter_info)
aliases: [t_promoter_info, mss.t_promoter_info]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 商户推广员信息表 (t_promoter_info)

## 用途
物理表 `mss.t_promoter_info`,主键 `id`。商户推广员信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `merchant_id` | varchar(20) | 推广员所属商户 |
| `member_id` | varchar(20) | 推官员对应mid |
| `mobile_no` | varchar(32) | 推广员手机号 · 可空 |
| `eid_num` | varchar(32) | 推广员eid · 可空 |
| `promoter_props` | varchar(200) | 实名和eid信息 · 可空 |
| `code_source` | varchar(32) | 推广员来源 · 可空 |
| `commissions_rates` | decimal(8, 4) | 推广员返佣比例 · 可空 |
| `commissions_type` | varchar(16) | 返佣类型 · 可空 |
| `invitation_status` | char(2) | 推广员状态 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_mid`:merchant_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

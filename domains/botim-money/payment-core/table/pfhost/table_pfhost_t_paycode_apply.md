---
id: tbl_pfhost_t_paycode_apply
object_type: Table
name: 付款码申请表 (t_paycode_apply)
aliases: [t_paycode_apply, pfhost.t_paycode_apply]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfhost schema DDL
tags: [payment-core, pfhost]
sensitivity: normal
related_services: []
---

# 付款码申请表 (t_paycode_apply)

## 用途
物理表 `pfhost.t_paycode_apply`,主键 `id`。付款码申请表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `member_id` | varchar(32) | 会员ID |
| `partner_id` | varchar(32) | 商户ID |
| `batch_no` | varchar(32) | 批次号 |
| `payment_no` | varchar(64) | 平台端支付订单号 |
| `card_token` | varchar(64) | 卡Token |
| `notify_url` | varchar(256) | 通知地址 · 可空 |
| `pcc_final` | varchar(256) | PCC_FINAL · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_payment_no`:payment_no
- `idx_payment_no_partner_id`:payment_no, partner_id
- `idx_pcc_final`:pcc_final

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

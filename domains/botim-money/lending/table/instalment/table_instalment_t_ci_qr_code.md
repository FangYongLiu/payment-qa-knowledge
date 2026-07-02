---
id: tbl_instalment_t_ci_qr_code
object_type: Table
name: t_ci_qr_code (t_ci_qr_code)
aliases: [t_ci_qr_code, instalment.t_ci_qr_code]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# t_ci_qr_code (t_ci_qr_code)

## 用途
物理表 `instalment.t_ci_qr_code`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 主健 · 可空 |
| `order_no` | varchar(64) | 订单号 |
| `user_id` | varchar(32) | 用户ID |
| `url` | varchar(100) | 二维码地址 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

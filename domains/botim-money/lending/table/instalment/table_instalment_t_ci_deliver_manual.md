---
id: tbl_instalment_t_ci_deliver_manual
object_type: Table
name: t_ci_deliver_manual (t_ci_deliver_manual)
aliases: [t_ci_deliver_manual, instalment.t_ci_deliver_manual]
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

# t_ci_deliver_manual (t_ci_deliver_manual)

## 用途
物理表 `instalment.t_ci_deliver_manual`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

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
| `deliver_url` | varchar(100) | 发货图片 |
| `imei_url` | varchar(100) | imei 图片 |
| `request_no` | varchar(100) | 流水号 |
| `status` | smallint(5) | 0 审核中 1 成功 -1 打回 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_request_no`:request_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

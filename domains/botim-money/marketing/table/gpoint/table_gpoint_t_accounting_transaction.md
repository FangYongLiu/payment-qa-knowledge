---
id: tbl_gpoint_t_accounting_transaction
object_type: Table
name: 记账事务 (t_accounting_transaction)
aliases: [t_accounting_transaction, gpoint.t_accounting_transaction]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 记账事务 (t_accounting_transaction)

## 用途
物理表 `gpoint.t_accounting_transaction`,主键 `transaction_id`。记账事务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transaction_id` | bigint | 事务ID：18位，固定41+10位时间戳+4位序列+2位随机 |
| `request_no` | varchar(32) | 请求号 |
| `client_id` | varchar(32) | 客户端id |
| `voucher_service` | int | 凭证服务 |
| `transaction_type` | varchar(10) | 事务类型：C=发行，D=销毁，T=转账 |
| `control_id` | bigint | 控制ID · 可空 |
| `control_identity` | varchar(32) | 控制标志 · 可空 |
| `biz_product_code` | varchar(10) | 业务产品码 · 可空 |
| `digest` | int | 事务摘要 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`transaction_id`
- `idx_create_time_client_id`:create_time, client_id
- `idx_request_no`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

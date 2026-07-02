---
id: tbl_invoice_t_invoice_order
object_type: Table
name: 收单数据 (t_invoice_order)
aliases: [t_invoice_order, invoice.t_invoice_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: invoice schema DDL
tags: [merchant-management, invoice]
sensitivity: normal
related_services: []
---

# 收单数据 (t_invoice_order)

## 用途
物理表 `invoice.t_invoice_order`,主键 `id`。收单数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 全局号 |
| `issuer_type` | varchar(32) | 发起人类型 |
| `issuer_code` | varchar(32) | 发起人代码 |
| `link_id` | varchar(64) | 链接id · 可空 |
| `es_id` | varchar(64) | 关联的es_id |
| `partner_id` | varchar(32) | 发起方memberId |
| `total_amount` | decimal(19, 4) | 收单金额 · 可空 |
| `tamt_currency_code` | varchar(8) | 收单币种 · 可空 |
| `notify_url` | varchar(200) | 商户通知地址 · 可空 |
| `sub_status` | varchar(32) | 收单状态 · 可空 |
| `status` | varchar(32) | 收单状态 |
| `acquire_order_id` | bigint | 收单订单id · 可空 |
| `due_time` | timestamp(3) | due_time · 可空 |
| `invoice_time` | timestamp(3) | invoice_time · 可空 |
| `file_path` | varchar(200) | 文件路径 · 可空 |
| `operator_id` | varchar(50) | 操作人ID · 可空 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `overdue_operation` | varchar(64) | overdueOperation · 可空 |
| `sended_count` | int | 已发送次数 |

## 主键 / 索引
- 主键:`id`
- `uk_ao_es`:es_id (UNIQUE)
- `uk_ao_lk`:link_id (UNIQUE)
- `i_ao_ct`:created_time
- `i_ao_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_ccexchange_t_fix_order
object_type: Table
name: 修正订单 (t_fix_order)
aliases: [t_fix_order, ccexchange.t_fix_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccexchange schema DDL
tags: [crypto, ccexchange]
sensitivity: normal
related_services: []
---

# 修正订单 (t_fix_order)

## 用途
物理表 `ccexchange.t_fix_order`,主键 `id`。修正订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `supplier_order_id` | varchar(50) | 供应商订单号 |
| `supplier_code` | varchar(32) | 供应商代码 |
| `merchant_mid` | varchar(32) | merchantMid |
| `status` | varchar(32) | status |
| `wrong_outer_order_id` | bigint | 错误订单号 |
| `revert_outer_order_id` | bigint | 冲正订单号 |
| `revert_trd_prm_id` | bigint | 冲正支付参数ID |
| `correct_trd_prm_id` | bigint | 冲正支付参数ID · 可空 |
| `correct_outer_order_id` | bigint | 冲正订单号 · 可空 |
| `symbol` | varchar(32) | symbol |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_fo_ct`:created_time
- `i_fo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_point_t_accounting_detail
object_type: Table
name: 记账明细 (t_accounting_detail)
aliases: [t_accounting_detail, point.t_accounting_detail]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: point schema DDL
tags: [marketing, point]
sensitivity: normal
related_services: []
---

# 记账明细 (t_accounting_detail)

## 用途
物理表 `point.t_accounting_detail`,主键 `accounting_id`。记账明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `accounting_id` | bigint | 记账id：18位，固定41+10位时间戳+4位序列+2位随机 |
| `request_no` | varchar(32) | 请求号 |
| `client_id` | varchar(32) | 客户端id |
| `operation_type` | varchar(10) | 操作类型：I=收入，TF=交易冻结，TUF=交易解冻，TUFO=交易解冻支出，TRI=交易退款收入，TO=交易支出，E=失效 |
| `orig_accounting_id` | bigint | 原记账id · 可空 |
| `accounting_type` | varchar(10) | 记账类型：I=收入，O=支出，F=冻结，UF=解冻，UFO=解冻支出 |
| `account_no` | bigint | 账户号 |
| `point_type` | varchar(10) | 点数类型 |
| `amount` | decimal(19, 4) | 操作数量 |
| `clearing_code` | varchar(64) | 清算编码 · 可空 |
| `remark` | varchar(255) | 备注 · 可空 |
| `before_available_amount` | decimal(19, 4) | 前可用数量 |
| `before_frozen_amount` | decimal(19, 4) | 前冻结数量 |
| `before_to_expire_available_amount` | decimal(19, 4) | 前待失效可用数量 |
| `before_to_expire_frozen_amount` | decimal(19, 4) | 前待失效冻结数量 |
| `after_available_amount` | decimal(19, 4) | 后可用数量 |
| `after_frozen_amount` | decimal(19, 4) | 后冻结数量 |
| `after_to_expire_available_amount` | decimal(19, 4) | 后待失效可用数量 |
| `after_to_expire_frozen_amount` | decimal(19, 4) | 后待失效冻结数量 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `accounting_version` | bigint | 记账版本 |
| `create_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`accounting_id`
- `idx_create_time_account_no_version`:create_time, account_no, accounting_version
- `idx_orig_accounting_id`:orig_accounting_id
- `idx_request_no`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

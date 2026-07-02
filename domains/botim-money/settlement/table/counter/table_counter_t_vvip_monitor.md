---
id: tbl_counter_t_vvip_monitor
object_type: Table
name: VVIP大额监控表 (t_vvip_monitor)
aliases: [t_vvip_monitor, counter.t_vvip_monitor]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# VVIP大额监控表 (t_vvip_monitor)

## 用途
物理表 `counter.t_vvip_monitor`,主键 `id`。VVIP大额监控表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `serial_number` | varchar(16) | 当日序号 |
| `file_name` | varchar(128) | 文件名 |
| `file_content` | varchar(1024) | 文件内容 · 可空 |
| `trade_time` | timestamp | 交易时间 · 可空 |
| `bank_account` | varchar(128) | 银行账户 · 可空 |
| `payer_name` | varchar(255) | 付款人名称 · 可空 |
| `payer_account` | varchar(128) | 付款人账号 · 可空 |
| `authorized_quota` | decimal(15, 2) | 授权额度 · 可空 |
| `direction` | char | 借贷方向 · 可空 |
| `amount` | decimal(15, 2) | 金额 |
| `currency` | char(3) | 币种 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_serial_number`:serial_number

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

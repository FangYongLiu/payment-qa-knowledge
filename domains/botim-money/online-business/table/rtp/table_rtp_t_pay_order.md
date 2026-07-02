---
id: tbl_rtp_t_pay_order
object_type: Table
name: Pay Order (t_pay_order)
aliases: [t_pay_order, rtp.t_pay_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rtp schema DDL
tags: [online-business, rtp]
sensitivity: normal
related_services: []
---

# Pay Order (t_pay_order)

## 用途
物理表 `rtp.t_pay_order`,主键 `pay_trade_no`。Pay Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `pay_trade_no` | bigint | Pay Trade No: voucher no |
| `member_id` | varchar(20) | Member Id |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency |
| `pay_status` | varchar(10) | Pay Status: P-Processing, F-Fail, S-Success |
| `pay_channel` | char(2) | Pay Channel · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`pay_trade_no`
- `idx_update_time_mid`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

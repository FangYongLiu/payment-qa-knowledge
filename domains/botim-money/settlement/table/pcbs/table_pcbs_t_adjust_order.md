---
id: tbl_pcbs_t_adjust_order
object_type: Table
name: Adjust Order (t_adjust_order)
aliases: [t_adjust_order, pcbs.t_adjust_order]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Adjust Order (t_adjust_order)

## 用途
物理表 `pcbs.t_adjust_order`,主键 `adjust_no`。Adjust Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `adjust_no` | bigint | Adjust No |
| `partner_id` | varchar(20) | Partner ID |
| `adjust_code` | varchar(10) | Adjustment Code: CLC=Customer Loading Collection, EBA=Escrow Balance Adjustment, PA=Profit Adjustment |
| `relate_id` | bigint | Relate ID · 可空 |
| `source_mid` | varchar(20) | Source Merchant ID |
| `source_acct_type` | varchar(20) | Source Account Type |
| `target_mid` | varchar(20) | Target Merchant ID |
| `target_acct_type` | varchar(20) | Target Account Type |
| `adjust_amount` | decimal(19, 4) | Adjust Amount |
| `currency` | char(3) | Currency |
| `status` | char | Status: P=Processing, S=Success, F=Failure, R=Retry |
| `trade_request_no` | bigint | Trade Request No · 可空 |
| `next_retry_time` | timestamp | Next Retry Time · 可空 |
| `retry_expire_time` | timestamp | Retry Expire Time · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension: allowRetry=Y/N · 可空 |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |

## 主键 / 索引
- 主键:`adjust_no`
- `idx_next_retry_time`:next_retry_time
- `idx_update_time_status`:update_time, status

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

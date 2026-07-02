---
id: tbl_transfer_t_settled_retry
object_type: Table
name: 结算重试表 (t_settled_retry)
aliases: [t_settled_retry, transfer.t_settled_retry]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 结算重试表 (t_settled_retry)

## 用途
物理表 `transfer.t_settled_retry`,主键 `settle_retry_no`。结算重试表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `settle_retry_no` | bigint | 结算重试交易号 |
| `settle_no` | bigint | 结算订单号 |
| `status` | char(2) | 结算重试状态: SP=处理中, SF=失败, SC=成功 |
| `gmt_created` | timestamp(3) | 创建时间 |
| `gmt_modified` | timestamp(3) | 修改时间 |

## 主键 / 索引
- 主键:`settle_retry_no`
- `idx_gmt_modified`:gmt_modified
- `idx_settle_no`:settle_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_ccceth_t_deposit_event_scanner
object_type: Table
name: 转账事件扫描器(不分区) (t_deposit_event_scanner)
aliases: [t_deposit_event_scanner, ccceth.t_deposit_event_scanner]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccceth schema DDL
tags: [crypto, ccceth]
sensitivity: normal
related_services: []
---

# 转账事件扫描器(不分区) (t_deposit_event_scanner)

## 用途
物理表 `ccceth.t_deposit_event_scanner`,主键 `chain_code`。转账事件扫描器(不分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `chain_code` | varchar(32) | 链代码 |
| `scanned_block_number` | bigint | 已扫描块高 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`chain_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

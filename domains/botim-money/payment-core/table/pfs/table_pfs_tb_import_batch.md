---
id: tbl_pfs_tb_import_batch
object_type: Table
name: 增长，10行/天 (tb_import_batch)
aliases: [tb_import_batch, pfs.tb_import_batch]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfs schema DDL
tags: [payment-core, pfs]
sensitivity: normal
related_services: []
---

# 增长，10行/天 (tb_import_batch)

## 用途
物理表 `pfs.tb_import_batch`,主键 `BATCH_ID`。增长，10行/天。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BATCH_ID` | decimal(15) | 批次Id |
| `CONTENT_TYPE` | varchar(128) | 内容类型 |
| `CONTENT_SOURCE` | varchar(256) | 数据来源 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `OPERATOR` | varchar(32) | 操作员 |
| `GMT_CREATE` | timestamp | 创建日期 |

## 主键 / 索引
- 主键:`BATCH_ID`
- `I_IMPORT_BATCH_CONTENTTYPE`:CONTENT_TYPE
- `I_IMPORT_BATCH_GMTCREATE`:GMT_CREATE

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

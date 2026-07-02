---
id: tbl_pfs_tb_import_detail
object_type: Table
name: 增长，100000行/天 (tb_import_detail)
aliases: [tb_import_detail, pfs.tb_import_detail]
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

# 增长，100000行/天 (tb_import_detail)

## 用途
物理表 `pfs.tb_import_detail`,主键 `DETAIL_ID`。增长，100000行/天。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `DETAIL_ID` | decimal(15) | 明细Id |
| `BATCH_ID` | decimal(15) | 批次Id |
| `CONTENT_TYPE` | varchar(128) | 内容类型 |
| `UPDATE_TYPE` | varchar(8) | 操作类型：Create=创建，Update=更新，Delete=删除 |
| `QUERY_FIELD` | varchar(128) | 查询域 |
| `OLD_DATA` | varchar(2000) | 旧数据 · 可空 |
| `NEW_DATA` | varchar(2000) | 新数据 · 可空 |
| `STATUS` | varchar(8) | 执行状态：Done=已执行，Wait=等待确认，Cancel=取消 |
| `AUDITOR` | varchar(32) | 审计员 · 可空 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`DETAIL_ID`
- `I_IMPORT_DETAIL_BATCHID`:BATCH_ID
- `I_IMPORT_DETAIL_CONTENTTYPE`:CONTENT_TYPE
- `I_IMPORT_DETAIL_GMTMODIFY`:GMT_MODIFY
- `I_IMPORT_DETAIL_QUERYFIELD`:QUERY_FIELD

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

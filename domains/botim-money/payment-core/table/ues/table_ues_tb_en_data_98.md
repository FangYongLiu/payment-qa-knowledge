---
id: tbl_ues_tb_en_data_98
object_type: Table
name: tb_en_data_98 (tb_en_data_98)
aliases: [tb_en_data_98, ues.tb_en_data_98]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ues schema DDL
tags: [payment-core, ues]
sensitivity: normal
related_services: []
---

# tb_en_data_98 (tb_en_data_98)

## 用途
物理表 `ues.tb_en_data_98`,主键 `None`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | unknown | 待补 · 可空 |
| `TICKET` | unknown | 待补 · 可空 |
| `STORAGE_TYPE` | unknown | 待补 · 可空 |
| `COMPRESS_ALGORITHM` | unknown | 待补 · 可空 |
| `ENCRYPT_KEY` | unknown | 待补 · 可空 |
| `ENCRYPT_DATA` | unknown | 待补 · 可空 |
| `VERSION` | unknown | 待补 · 可空 |
| `CREATE_TIME` | unknown | 待补 · 可空 |
| `LAST_UPDATE_TIME` | unknown | 待补 · 可空 |
| `ENCRYPT_TYPE` | unknown | 待补 · 可空 |

## 主键 / 索引
- 主键:`None`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

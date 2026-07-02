---
id: tbl_ues_tb_task
object_type: Table
name: tb_task (tb_task)
aliases: [tb_task, ues.tb_task]
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

# tb_task (tb_task)

## 用途
物理表 `ues.tb_task`,主键 `None`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | unknown | 待补 · 可空 |
| `FROM_ID` | unknown | 待补 · 可空 |
| `TO_ID` | unknown | 待补 · 可空 |
| `RUN_BY` | unknown | 待补 · 可空 |
| `STATE` | unknown | 待补 · 可空 |
| `START_TIME` | unknown | 待补 · 可空 |
| `END_TIME` | unknown | 待补 · 可空 |
| `CREATE_TIME` | unknown | 待补 · 可空 |
| `LOCK_VERSION` | unknown | 待补 · 可空 |
| `UPDATE_TIME` | unknown | 待补 · 可空 |

## 主键 / 索引
- 主键:`None`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

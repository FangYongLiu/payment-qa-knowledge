---
id: tbl_creditues_tb_certification
object_type: Table
name: tb_certification (tb_certification)
aliases: [tb_certification, creditues.tb_certification]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditues schema DDL
tags: [lending, creditues]
sensitivity: normal
related_services: []
---

# tb_certification (tb_certification)

## 用途
物理表 `creditues.tb_certification`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint | 主键 · 可空 |
| `CERTIFICATION_PATH` | varchar(256) | 证书路径 |
| `CREATE_TIME` | timestamp | 创建时间 |
| `CERTIFICATION_PASSWORD` | varchar(128) | 证书密码（不能为空） · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

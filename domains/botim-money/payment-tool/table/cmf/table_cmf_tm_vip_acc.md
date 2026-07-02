---
id: tbl_cmf_tm_vip_acc
object_type: Table
name: vip 账户列表 (tm_vip_acc)
aliases: [tm_vip_acc, cmf.tm_vip_acc]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# vip 账户列表 (tm_vip_acc)

## 用途
物理表 `cmf.tm_vip_acc`,主键 `ACC_NO`。vip 账户列表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ACC_NO` | varchar(64) | 账户 |

## 主键 / 索引
- 主键:`ACC_NO`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

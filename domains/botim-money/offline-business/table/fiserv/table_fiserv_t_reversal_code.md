---
id: tbl_fiserv_t_reversal_code
object_type: Table
name: 需要发起冲正的消息列表 (t_reversal_code)
aliases: [t_reversal_code, fiserv.t_reversal_code]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fiserv schema DDL
tags: [offline-business, fiserv]
sensitivity: normal
related_services: []
---

# 需要发起冲正的消息列表 (t_reversal_code)

## 用途
物理表 `fiserv.t_reversal_code`,主键 `id`。需要发起冲正的消息列表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `code` | varchar(512) | 需要重试的信息内容 |
| `short_code` | varchar(32) | 需要重试的返回码缩写 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

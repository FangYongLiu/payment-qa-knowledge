---
id: tbl_mchtsettle_t_black_list
object_type: Table
name: merchant black list (t_black_list)
aliases: [t_black_list, mchtsettle.t_black_list]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# merchant black list (t_black_list)

## 用途
物理表 `mchtsettle.t_black_list`,主键 `merchant_mid`。merchant black list。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `merchant_mid` | varchar(50) | merchant_mid |

## 主键 / 索引
- 主键:`merchant_mid`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

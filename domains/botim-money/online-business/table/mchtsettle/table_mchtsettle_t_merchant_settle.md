---
id: tbl_mchtsettle_t_merchant_settle
object_type: Table
name: merchant settle (t_merchant_settle)
aliases: [t_merchant_settle, mchtsettle.t_merchant_settle]
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

# merchant settle (t_merchant_settle)

## 用途
物理表 `mchtsettle.t_merchant_settle`,主键 `merchant_mid`。merchant settle。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `merchant_mid` | varchar(50) | merchantMid |
| `created_time` | timestamp(3) | created_time |

## 主键 / 索引
- 主键:`merchant_mid`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

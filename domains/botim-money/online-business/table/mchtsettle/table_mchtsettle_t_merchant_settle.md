---
id: tbl_mchtsettle_t_merchant_settle
object_type: Table
name: 商户结算开通表 (t_merchant_settle)
aliases: [t_merchant_settle, mchtsettle.t_merchant_settle]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, 商户结算, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# 商户结算开通表 (t_merchant_settle)

## 用途
物理表 `mchtsettle.t_merchant_settle`,主键 `merchant_mid`。merchant settle。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
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
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **商户维度**:`merchant_mid` 为商户号,按商户聚合/对账。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。

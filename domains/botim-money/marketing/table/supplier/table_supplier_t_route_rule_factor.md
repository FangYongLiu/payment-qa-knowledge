---
id: tbl_supplier_t_route_rule_factor
object_type: Table
name: 供应商渠道路由要素 (t_route_rule_factor)
aliases: [t_route_rule_factor, supplier.t_route_rule_factor]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 供应商渠道路由要素 (t_route_rule_factor)

## 用途
物理表 `supplier.t_route_rule_factor`,主键 `ID`。供应商渠道路由要素。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(32) | 待补 · 可空 |
| `FACTOR_NO` | varchar(32) | 要素编号 |
| `FACTOR_NAME` | varchar(32) | 要素名称 |
| `FACTOR_WEIGHT` | decimal(3) | 要素权重 |
| `SUPPLIER_CHANNEL_CODE` | varchar(32) | 供应商渠道代码 |
| `Commission_TYPE` | varchar(1) | 佣金类型：G（groovy），R（rate比率）,E(each每笔) · 可空 |
| `Commission_CONTENT` | varchar(2048) | 佣金计算表达式 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |

## 主键 / 索引
- 主键:`ID`
- `uk_channelCode`:SUPPLIER_CHANNEL_CODE (UNIQUE)
- `uk_factorNo`:FACTOR_NO (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_deposit_t_trade_param
object_type: Table
name: 交易参数配置表 (t_trade_param)
aliases: [t_trade_param, deposit.t_trade_param]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# 交易参数配置表 (t_trade_param)

## 用途
物理表 `deposit.t_trade_param`,主键 `ID`。交易参数配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | varchar(11) | 交易参数配置ID，主键，YYYY+SEQ_TRADE_PARAM |
| `BIZ_PRODUCT_CODE` | varchar(32) | 产品编码 · 可空 |
| `PRODUCT_LAB` | varchar(128) | 产品标签 · 可空 |
| `PARAM_TYPE` | varchar(16) | 参数类型 |
| `PARAM_KEY` | varchar(32) | 参数KEY |
| `PARAM_VALUE` | varchar(128) | 参数VALUE · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`ID`
- `UK_PARAM_PRODUCT_KEY`:BIZ_PRODUCT_CODE, PARAM_KEY (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_payment_tb_refresh
object_type: Table
name: 稳定，100行 (tb_refresh)
aliases: [tb_refresh, payment.tb_refresh]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 稳定，100行 (tb_refresh)

## 用途
物理表 `payment.tb_refresh`,主键 `REFRESH_ID`。稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `REFRESH_ID` | decimal(15) | 主键 |
| `REFRESH_CODE` | varchar(128) | 刷新内容标识 |
| `IP_ADDRESS` | varchar(15) | IP地址 |
| `NEED_REFRESH` | char | 是否需要刷新，Y=需要，N=不需要 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 最近刷新时间 |

## 主键 / 索引
- 主键:`REFRESH_ID`
- `UK_REFRESH_CODE_IP`:REFRESH_CODE, IP_ADDRESS (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

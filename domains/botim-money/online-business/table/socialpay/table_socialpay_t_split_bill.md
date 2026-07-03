---
id: tbl_socialpay_t_split_bill
object_type: Table
name: AA收款账单表 (t_split_bill)
aliases: [t_split_bill, socialpay.t_split_bill]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: socialpay schema DDL
tags: [online-business, socialpay]
sensitivity: normal
related_services: [svc_socialpay]
---

# AA收款账单表 (t_split_bill)

## 用途
物理表 `socialpay.t_split_bill`,主键 `ID`。AA收款账单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(17) | 待补 |
| `BILL_NO` | varchar(32) | AA账单号 外部传入 唯一 |
| `PAYEE_UID` | varchar(50) | 收款人Totok的UID |
| `BILL_AMOUNT` | decimal(15, 4) | 收款金额 |
| `TYPE` | varchar(16) | AA收款类型：SPECIFIED:指定金额、IDENTICAL:相同金额 · 可空 |
| `RECEIVED_AMOUNT` | decimal(15, 4) | 已收款金额 |
| `CURRENCY_CODE` | varchar(8) | 币种 |
| `ITEM_COUNT` | int(10) | 参与人数 |
| `BILL_MEMO` | varchar(255) | 账单备注 · 可空 |
| `STATUS` | varchar(16) | PROCESSING（处理中）、FINISH（订单结束） |
| `GMT_CREATE` | timestamp | 提交时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `NOTIFY_PARAM` | varchar(2000) | 通知参数 透传到totok · 可空 |

## 主键 / 索引
- 主键:`ID`
- `BILL_NO`:BILL_NO (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_transferii_t_cancel_order
object_type: Table
name: 取消订单表 (t_cancel_order)
aliases: [t_cancel_order, Cancel Order]
domain: wallet
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags: [transferii, send-money, cancel-order]
related_services: [svc_transfer]
related_scenarios: []
---

# 取消订单表 (t_cancel_order)

## 用途
位于 `transferii` schema,记录 Send Money 场景下钱包订单的取消动作,与 [[tbl_transferii_t_wallet_order]]、[[tbl_transferii_t_party_order]] 配合形成订单生命周期数据模型。过期退款流程见 [[flow_wallet_send_money]]。

## 关联关系
- **所属服务**:transfer(待补,未建 Service 对象)
- **关联主表**:[[tbl_transferii_t_wallet_order]](通过 `wallet_order_no`)
- **同模型表**:[[tbl_transferii_t_party_order]]、[[tbl_transferii_t_order_permit]]

## 关键列
| 列名 | 说明 |
|---|---|
| cancel_order_no | Cancel Order 编号(原文图片在此字段处截断,类型未给出) |

> 注:原文图片在该表字段列表处截断,仅可见 `cancel_order_no` 一列;其余字段(如取消原因、操作人、时间戳、状态)未在原文出现 —— **待补**。

## 主键 / 索引
- 主键:`cancel_order_no`(依据可见部分推断;原文未显式标注 PK)。待补:其余索引未提供。

## 校验点(QA 关注)
- 取消记录应可关联到对应 `t_wallet_order.wallet_order_no`,验证取消链路完整。
- 与 `t_party_order` 的状态联动:取消发生时,相关参与方订单状态应同步流转。
- 原文未提供更多字段,QA 验证时以实际 DDL 为准,不应基于本文档假设字段存在。

---
id: svc_cash_eatm
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp058
name: cash-eatm
dev_owner: Sijia.Zhang
aliases: [gp058_cash-eatm]
related_services: []
related_tables: []
---

# cash-eatm

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp058` · domain=`online-business`。

## 作用
**现金 / ATM 业务**服务(gp058)。处理四类现金订单:**现金存入(CashIn)/ 取现(CashOut)/ 现金派送(CashDelivery)/ 现金充值(CashTopUp)**,各自状态机由定时 job 推进,并做账单同步。

## 系统中的位置
- 功能层:收单业务线(现金 / ATM)
- 业务域:`online-business`
- 驱动方式:定时 job 推进订单 + 账单同步(本窗口无同步 `*ClientImpl` 下游)。

## 关联关系
以订单状态机 + 定时 job 为主;`BillDataSyncFacadeImpl` 做账单数据同步。无同步 RPC 下游(本窗口)。

## 关键方法 / 入口(UAT 实测 mClass)
- `CashInOrderAutoAdvanceJob` / `CashOutOrderAutoAdvanceJob` / `CashDeliveryOrderAutoAdvanceJob` / `CashTopUpOrderAutoAdvanceJob` —— 四类现金订单自动推进。
- `BillDataSyncFacadeImpl` —— 账单数据同步。

## 测试要点 / 排障 / 常见问题
- 四类订单(存/取/派送/充值)各自状态机推进正确性;job 幂等。
- 账单同步一致性;落库 `casheatm` 库(见下)订单/锁表状态。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp058` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `casheatm` 库(22 张,见 `online-business/table/casheatm/`)。主要表:[[tbl_casheatm_t_cash_delivery_order]] · [[tbl_casheatm_t_cash_in_order]] · [[tbl_casheatm_t_cash_out_order]] · [[tbl_casheatm_t_cash_top_up_order]] · [[tbl_casheatm_t_trade_order_lock]] · [[tbl_casheatm_t_trade_order_ref]]。

---
id: svc_merchant_settlement
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp288
name: merchant-settlement
dev_owner: Shuo.Wang
aliases: [gp288_merchant-settlement]
related_services: []
related_tables: []
---

# merchant-settlement

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp288` · domain=`online-business`。

## 作用
商户结算（被 statementii 调用，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`online-business`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
statementii

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp288` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `mchtsettle` 库(21 张,见 `online-business/table/mchtsettle/`)。主要表:[[tbl_mchtsettle_t_black_list]] · [[tbl_mchtsettle_t_channel_summary]] · [[tbl_mchtsettle_t_clearing_batch]] · [[tbl_mchtsettle_t_clearing_detail]] · [[tbl_mchtsettle_t_clearing_file]] · [[tbl_mchtsettle_t_clearing_fileline]]。

---
id: svc_pix
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp261
name: pix
dev_owner: Yu.Tang,Xiaoyu.Sun
aliases: [gp261_pix]
related_services: [svc_marketing]
related_tables: []
---

# pix

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp261` · domain=`payment-core`。

## 作用
pix  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_marketing]] marketing（营销服务） · 7076 次 · high

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_pix_mpc_create_trade]] MPC创建交易接口 (/pix/mpc/v1/create-trade)、[[api_pix_mpc_get_rules]] 查询MPC匹配规则接口 (/pix/mpc/v1/get-rules)、[[api_pix_mpc_parse]] MPC解析接口 (/pix/mpc/v1/parse)
**读写的表:** [[tbl_pix_refund_transaction]] PIX退款交易表 t_refund_transaction、[[tbl_pix_t_refund_transaction]] PIX退款交易表 t_refund_transaction、[[tbl_pix_t_fx_config]] PIX FX配置表 t_fx_config、[[tbl_pix_trade_transaction]] PIX交易表 t_trade_transaction、[[tbl_pix_t_trade_transaction]] PIX交易表 t_trade_transaction、[[tbl_pix_t_trade_relate_order]] pix交易关联订单表 t_trade_relate_order、[[tbl_pix_t_trade_transaction_extend]] PIX交易扩展表 t_trade_transaction_extend、[[tbl_pix_db]] pix库交易核心表、[[tbl_pix_t_fx_rate_version]] PIX FX汇率版本表 t_fx_rate_version、[[tbl_pix_trade_transaction_extend]] PIX交易扩展表 t_trade_transaction_extend、[[tbl_pix_trade_relate_order]] PIX交易关联订单表 t_trade_relate_order、[[tbl_pix_t_fx_margin_version]] PIX FX Margin版本表 t_fx_margin_version

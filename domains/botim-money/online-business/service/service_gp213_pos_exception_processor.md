---
id: svc_pos_exception_processor
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp213
name: pos-exception-processor
subdomain: acquiring
dev_owner: Sijia.Zhang
aliases: [gp213_pos-exception-processor]
related_services: []
related_tables: []
---

# pos-exception-processor

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp213` · domain=`online-business`。

## 作用
**POS 异常订单处理**服务(gp213):处理线下 POS 收单产生的异常订单(`t_exception_order`),以定时 job 自动推进异常单的处理/冲正。

## 系统中的位置
- 功能层:收单业务线(线下 POS 异常处理)
- 业务域:`online-business`
- 驱动方式:定时 job 推进异常订单。

## 关联关系
异常订单以本地状态机 + `ExceptionOrderAutoAdvanceJob` 推进;与线下 POS 被扫收单流程相关(见 [[flow_pos_scan_payment_code]] / [[scn_online_business_payment_code_scan]])。

## 关键方法 / 入口(UAT 实测 mClass)
- `ExceptionOrderAutoAdvanceJob` —— 异常订单自动推进/处理。

## 测试要点 / 排障 / 常见问题
- 造 POS 异常单(超时/中断/重复)后,job 是否正确推进到终态(冲正/成功/失败)。
- job 幂等与重复执行;落库 `posexception` 库 `t_exception_order` 状态。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp213` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `posexception` 库(3 张,见 `online-business/table/posexception/`)。主要表:[[tbl_posexception_t_exception_order]]。

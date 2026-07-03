---
id: svc_preauth
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp197
name: preauth
subdomain: acquiring
dev_owner: Sijia.Zhang
aliases: [gp197_preauth]
related_services: []
related_tables: []
---

# preauth

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp197` · domain=`online-business`。

## 作用
**预授权(PreAuth)业务**服务(gp197):管理预授权订单全生命周期——预授权(preauth)、请款完成(completion)、撤销(reversal / void)、金额更新(update)。是收单 `PREAUTH` / `CAPTURE` / `PREAUTHVOID` 支付场景的后端订单服务。

## 系统中的位置
- 功能层:收单业务线(预授权 / 请款 / 撤销)
- 业务域:`online-business`
- 驱动方式:订单状态机 + 定时 job 推进。

## 关联关系
预授权订单生命周期以本地状态机 + `CompletionOrderAutoAdvanceJob` 推进;收单入口经 [[svc_acquireii]] 的 PREAUTH/CAPTURE/PREAUTHVOID 场景。场景见 [[scn_online_business_pre_auth]],请求样例见 [[reference_acquire_payscene_request_examples]]。

## 关键方法 / 入口(UAT 实测 mClass)
- `CompletionOrderAutoAdvanceJob` —— 请款完成单自动推进。
- 订单类型(库表):`t_preauth_order`(预授权)/ `t_completion_order`(请款)/ `t_reversal_order`(撤销)/ `t_void_ops_order`(Void)/ `t_update_preauth_order`(改额)。

## 测试要点 / 排障 / 常见问题
- **预授权全流程**:PREAUTH 冻结 → CAPTURE 请款 → 或 PREAUTHVOID 撤销;各订单状态机推进。
- 部分请款 / 多次请款、超时自动撤销(job);改额边界。
- 落库 `preauth` 库(见下)各订单表状态一致。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp197` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `preauth` 库(16 张,见 `online-business/table/preauth/`)。主要表:[[tbl_preauth_t_completion_order]] · [[tbl_preauth_t_preauth_order]] · [[tbl_preauth_t_reversal_order]] · [[tbl_preauth_t_terminal_detail]] · [[tbl_preauth_t_update_preauth_order]] · [[tbl_preauth_t_void_ops_order]]。

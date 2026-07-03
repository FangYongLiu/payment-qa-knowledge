---
id: svc_socialpay
object_type: Service
domain: online-business
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp035
name: socialpay
dev_owner: Guoyou.Ma
aliases: [gp035_socialpay]
related_services: [svc_member]
related_tables: []
---

# socialpay

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp035` · domain=`online-business`。

## 作用
**社交支付**服务(gp035):红包(`t_redpkg_order`)与社交转账(`t_transfer_order`)。以发号器 + 补偿事件重试 + 过期分账单处理驱动。

## 系统中的位置
- 功能层:收单业务线(社交支付 / 红包 / 转账)
- 业务域:`online-business`

## 关联关系
**下游**:[[svc_member]](`MemberClient`,查会员/账户)。补偿事件与过期处理由本地 job 驱动。

## 关键方法 / 入口(UAT 实测 mClass)
- `SegmentIDGenImpl` —— 分段发号器(订单号生成)。
- `CompensationEventJob` / `CompensationEventRetryServiceImpl` —— 补偿事件与重试(最终一致)。
- `SplitBillForExpireJob` —— 分账单过期处理。
- `MemberClient` —— 调 [[svc_member]]。

## 参与的业务场景(cgs 回归)
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 测试要点 / 排障 / 常见问题
- 红包 / 转账订单创建与状态流转;发号器唯一性。
- **补偿与重试**:异常后补偿事件是否触发、重试幂等、最终一致。
- 分账单过期回收;落库 `socialpay` 库(见下)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp035` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `socialpay` 库(7 张,见 `online-business/table/socialpay/`)。主要表:[[tbl_socialpay_t_redpkg_order]] · [[tbl_socialpay_t_transfer_order]]。

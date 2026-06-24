---
id: scn_wallet_account_mgmt
object_type: Scenario
name: 账户 / 会员管理 (Account & Member)
aliases: []
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [wallet, cgs-apitest]
related_services: [svc_member, svc_cgs, svc_sgs, svc_kyc]
related_tables: []
related_logs: []
---

# 账户 / 会员管理 (Account & Member)

> 业务测试场景。来源 cgs-apitest 回归。

## 场景描述
toC 账户与会员管理:登录、会员信息查询/维护、密码(设置/修改/校验)、注销账户、换绑手机。经 cgs/sgs 网关 + member 会员核心(换绑手机触达 kyc)。

## 关联关系
- **涉及服务**:[[svc_member]]、[[svc_cgs]]、[[svc_sgs]]、[[svc_kyc]](= `related_services`)
- **覆盖的自动化**:见各 [[auto_*]]
- **读写的表**:待补

## 校验点(QA)
- 登录态/token;密码设置-修改-校验流转。
- 注销账户后状态与数据;换绑手机新旧号一致性(touch kyc)。
- 会员信息查询脱敏;落库 member 状态。

## 来源与置信
- cgs-apitest 套件整理;服务链由调用线索+callgraph 推断,部分待补。

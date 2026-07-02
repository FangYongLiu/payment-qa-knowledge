---
id: scn_grc_identity_3ds_rule
object_type: Scenario
name: 风控核身规则配置控制3DS触发
aliases: []
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1057685568
tags:
- 3ds
- identity-rule
- core-identity
related_services:
- svc_grc_check_identity_provider
---

# 风控核身规则配置控制3DS触发

## 触发/入口
支付场景下是否触发 3DS 核身验证由风控核身规则决定。在 SIM/Basis 环境通过"核身规则管理"配置该规则,由核身服务 [[svc_grc_check_identity_provider]] 执行。

配置路径:Basis → RISK CONTROL → Risk Event → Identity Rule Management。审核入口在 Basis `GENERAL → General Audit → Audit Record`(`AuditType = GRC_IDENTITY_RULE`)。

## 关联关系
- **涉及服务**:[[svc_grc_check_identity_provider]](= `related_services`,核身规则缓存 key)
- **管理后台**:Basis Admin([[auto_basis_visual_rule_admin]]) 核身规则管理 + General Audit 审核记录页

## 前置条件
- 已具备 Basis 后台访问权限。
- 明确目标支付场景是否应触发 3DS。

## 操作步骤
1. 在 Identity Rule Management 新增/编辑核身规则,关键字段:
   - `EventType`:风控事件,如 `PAYMENT`
   - `IdentityRule`:规则条件,如 `payAmount>=10`(或 `riskScore<=1000`、`isNeedIdentifyHint=='Y'` 等)
   - `IdentityCheckType`:多条件关系,如 `&&`
   - `IdentityType`:核身方式,如 `THREEDS`
   - `Priority`:优先级,值越小优先级越高
2. 提交规则的新增/生效/停用 → 在 General Audit → Audit Record 完成二次审核(`AuditStatus` 从 `WAITING` 到通过)。
3. 审核通过后清除 Redis 缓存(缓存 key:`gp079_grc-check-identity-provider`),配置才真正生效(两种清理方法任选其一)。
4. 发起对应支付场景,观察是否按规则触发 3DS。

## DB 校验点
- 核身规则列表中目标规则状态为 `Active`、条件/IdentityType/Priority 符合预期。
- 待补:核身规则底层物理表原文未提供。

## 预期结果
- 命中规则条件的支付场景按 `IdentityType`(如 `THREEDS`)触发对应核身;未命中则不触发。
- 新增/生效/停用均需经审核;审核通过后必须清 `gp079_grc-check-identity-provider` 缓存才生效,否则仍为旧行为。

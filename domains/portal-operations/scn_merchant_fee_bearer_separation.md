---
id: scn_merchant_fee_bearer_separation
object_type: Scenario
name: 收支分离商户配置(独立 MID 扣手续费)
aliases: [fee bearer separation, 收支分离, fee_bearer 配置]
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'confluence:AQ/1082425488, wiki:52e73b6f'
tags: [basis, merchant-setting, fee-bearer, acs]
related_services: [svc_basis]
related_tables: []
related_logs: []
related_requirements: [PAYM-1068]
---

# 收支分离商户配置(独立 MID 扣手续费)

## 触发 / 入口
在 Basis 系统中通过 `Merchant Setting` 为指定商户配置独立 MID，使其在**充值 / 出款**场景中由另一个商户账户承担手续费，实现交易发起方与手续费扣款方的账户分离。需求 PAYM-1068。

## 关联关系
- **涉及服务**:[[svc_basis]](= `related_services`)
- **关联需求**:PAYM-1068(= `related_requirements`)
- **配置审核入口**:Basis General Audit，见 [[ref_bmoc_basis_merchant]]

## 前置条件
- 已确定交易发起方 MID 与实际扣手续费的商户 MID。
- 知道业务产品码 `bizProductCode`。

## 操作步骤
在 Basis 系统新增一条 `Merchant Setting` 记录:

| 字段 | 示例值 | 含义 |
| --- | --- | --- |
| MerchantId | `200000430641` | 交易发起方 MID(配置作用对象) |
| ParamKey | `fee_bearer_230502` | 规则 `fee_bearer_${bizProductCode}` |
| ParamValue | `200000431881\|BASIC` | 实际扣手续费的商户，规则 `${MerchantId}\|${AccountType}` |

提交后需经过审核流程，审核通过配置才生效(General Audit → Audit Record，列表按 `AuditId` 搜索，待审记录提供 `Audit` 按钮;`AuditInfo` 区 `MerchantId`/`ParamKey` 只读)。

## DB 校验点
- 配置落库表:`acs.t_merchant_setting`。
- 校验 ParamKey 前缀 `fee_bearer_` 拼接正确的 `bizProductCode`，ParamValue 中 MID 与 AccountType 用 `|` 拼接。

## 预期结果
- 充值/出款场景下手续费由 ParamValue 指定的商户账户扣除。
- 审核未通过前配置不生效。

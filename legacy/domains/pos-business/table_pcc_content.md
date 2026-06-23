---
id: tbl_pcc_content
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_pcc_content.md
tags:
- PCC
- 支付授权凭证
- 付款码
- 风控
subdomain: null
module: null
sensitivity: normal
name: 支付授权凭证表
aliases:
- t_pcc_content
- acquireii.t_pcc_content
- PCC
related_services: []
related_tables:
- tbl_fiserv_sale_order
- tbl_pcc_content_param
related_scenarios:
- scn_merchant_transaction_db_check
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

**PCC = Payment Credential Code**，即**支付授权凭证**，存储 PayBy 支付授权凭证核心信息。该表是 PayBy APP 生成付款码的核心载体，承载付款码字符串、用户选择的支付渠道以及风控评分等关键数据。

- 表名：`acquireii.t_pcc_content`
- 体系定位：用户侧付款码生成 → 商户侧扫码受理（POS/扫码枪）→ 收单侧风控与支付链路

## 在交易链路中的位置

```
用户在 PayBy APP 生成付款码
   └─> t_pcc_content (本表)         ← 存储 pcc_final / pay_method / risk_level
         └─> t_pcc_content_param   ← 1:N 扩展参数

商户扫码（POS / 扫码枪）受理付款码
   └─> 解析 pcc_final → 进入收单交易（如 Fiserv 销售订单 tbl_fiserv_sale_order 等）
         └─> 风控基于 risk_level 决定是否额外验证
```

**典型场景**：
- 用户在 PayBy APP 生成付款码（写入本表）
- 商户扫码（POS 机/扫码枪）识别付款码（读取本表）
- 风控基于 `risk_level` 检查付款码风险

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | **主键**，全局 ID，与 `t_pcc_content_param` 关联 |
| `pcc_final` | varchar(200) | ✅ | 授权码字符串（最终二维码内容），**敏感数据** |
| `pay_method` | varchar(200) |  | 用户选择的支付渠道（非最终成功渠道） |
| `risk_level` | varchar(200) |  | 风险级别（风控评分），如 `LOW`/`HIGH`/`CRITICAL` |

## 主键/索引

- 主键：`global_id`

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |

## 关联表

| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|---------|------|
| `t_pcc_content_param` | 1:N | `global_id` | 授权凭证扩展参数 |
| `tbl_fiserv_sale_order` | 业务下游 | 通过付款码触发的销售单 | 商户扫码后的实际收单交易落库 |

## QA 落库检查要点

1. **付款码生成校验**：用户在 APP 生成付款码后，检查 `t_pcc_content` 是否插入新记录，`global_id` 与 `pcc_final` 必须存在且非空。
2. **pcc_final 敏感性**：付款码字符串属敏感数据，**不可日志泄露 / 不可在非授权接口返回**，QA 验证日志与接口响应是否脱敏。
3. **风险级别影响支付流程**：当 `risk_level` 为 `HIGH` / `CRITICAL` 时，需验证支付流程是否触发额外验证（如二次确认 / 拒绝）。
4. **pay_method 语义**：该字段是**用户选择的**支付渠道，**不代表最终成功使用的渠道**，对账与统计时需注意区分。
5. **JOIN 扩展参数**：查询完整授权凭证信息时，需 `LEFT JOIN t_pcc_content_param ON global_id`，避免漏取扩展参数。
6. **链路串联**：付款码被 POS / 扫码枪受理后，应能通过业务流水反查到 `t_pcc_content.global_id`，并最终在收单订单表（如 `tbl_fiserv_sale_order`）中找到对应交易记录。

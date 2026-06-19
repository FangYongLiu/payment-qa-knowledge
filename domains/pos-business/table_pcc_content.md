---
id: tbl_pcc_content
object_type: Table
domain: device-pos
status: active
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
- tbl_pcc_content_param
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

PCC = Payment Credential Code，**支付授权凭证**，存储 PayBy 支付授权凭证核心信息。

表名：`acquireii.t_pcc_content`

**典型场景**：
- 用户在 PayBy APP 生成的付款码
- 商户扫码识别付款码
- 风控检查付款码的风险级别

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | **主键**，全局 ID |
| `pcc_final` | varchar(200) | ✅ | 授权码字符串（最终二维码内容） |
| `pay_method` | varchar(200) |  | 选择的支付渠道 |
| `risk_level` | varchar(200) |  | 风险级别（风控评分） |

## 主键/索引

- 主键：`global_id`
- 索引：

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |

- 关联表：`t_pcc_content_param`（1:N，关联字段 `global_id`）

## 校验点(QA 关注)

1. **pcc_final 是敏感数据**：用户付款码不能泄露
2. **风险级别影响支付流程**：高风险（`HIGH`、`CRITICAL`）可能需要额外验证
3. **pay_method 是用户选择的，不是最终成功的**
4. 查询授权凭证及参数时，需 LEFT JOIN `t_pcc_content_param` ON `global_id`

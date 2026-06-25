---
id: tbl_pcc_content
object_type: Table
name: 支付授权凭证表(acquireii.t_pcc_content)
aliases:
- t_pcc_content
- acquireii.t_pcc_content
- PCC
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_pcc_content.md
tags:
- PCC
- 支付授权凭证
- 付款码
- 风控
related_services: [svc_acquireii]
related_scenarios: []
---

# 支付授权凭证表(acquireii.t_pcc_content)

## 用途
**PCC = Payment Credential Code**，即支付授权凭证，存储 PayBy 支付授权凭证核心信息。该表是 PayBy APP 生成付款码的核心载体，承载付款码字符串、用户选择的支付渠道及风控评分等关键数据。体系定位:用户侧付款码生成 → 商户侧扫码受理(POS/扫码枪) → 收单侧风控与支付链路。

库表:`acquireii.t_pcc_content`。典型场景:用户在 PayBy APP 生成付款码(写入本表) → 商户扫码(POS 机/扫码枪)识别付款码(读取本表) → 风控基于 `risk_level` 检查付款码风险 → 进入收单交易(如 [[tbl_fiserv_sale_order]])。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`,tbl→service 边)。
- **关键表**:`t_pcc_content_param`(1:N，授权凭证扩展参数，对象待补)、[[tbl_fiserv_sale_order]](付款码受理后的实际收单交易落库)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]]);另涉及商户交易落库检查、付款码被 POS/扫码枪扫等场景(对象待补)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint ✅ | 主键，全局 ID，与 `t_pcc_content_param` 关联 |
| `pcc_final` | varchar(200) ✅ | 授权码字符串(最终二维码内容)，**敏感数据** |
| `pay_method` | varchar(200) | 用户选择的支付渠道(非最终成功渠道) |
| `risk_level` | varchar(200) | 风险级别(风控评分)，如 `LOW`/`HIGH`/`CRITICAL` |

## 主键 / 索引
- 主键:`global_id`(PRIMARY)。

## 校验点(QA 关注)
- **付款码生成校验**:用户在 APP 生成付款码后，检查本表是否插入新记录，`global_id` 与 `pcc_final` 必须存在且非空。
- **pcc_final 敏感性**:付款码字符串属敏感数据，**不可日志泄露 / 不可在非授权接口返回**，验证日志与接口响应是否脱敏。
- **风险级别影响支付流程**:`risk_level` 为 `HIGH` / `CRITICAL` 时，需验证是否触发额外验证(二次确认 / 拒绝)。
- **pay_method 语义**:该字段是**用户选择的**支付渠道，**不代表最终成功使用的渠道**，对账与统计时需区分。
- **JOIN 扩展参数**:查询完整授权凭证信息需 `LEFT JOIN t_pcc_content_param ON global_id`，避免漏取扩展参数。
- **链路串联**:付款码被 POS / 扫码枪受理后，应能通过业务流水反查到本表 `global_id`，并最终在收单订单表(如 [[tbl_fiserv_sale_order]])找到对应交易。

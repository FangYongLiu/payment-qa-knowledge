---
id: tbl_payment_tb_fund_ctl_order
object_type: Table
name: tb_fund_ctl_order (tb_fund_ctl_order)
aliases: [tb_fund_ctl_order, payment.tb_fund_ctl_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# tb_fund_ctl_order (tb_fund_ctl_order)

## 用途
物理表 `payment.tb_fund_ctl_order`,主键 `CTL_VOUCHER_NO`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CTL_VOUCHER_NO` | varchar(32) | 控制凭证号 |
| `REL_CTL_VOUCHER_NO` | varchar(32) | 关联控制凭证号 · 可空 |
| `CTL_TYPE` | varchar(16) | 冻结：FREEZE,解冻UNFREEZE |
| `MEMBER_ID` | varchar(32) | 会员ID · 可空 |
| `PARTNER_ID` | varchar(32) | 平台方ID · 可空 |
| `AMOUNT` | decimal(15, 4) | 金额 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `STATUS` | char | P处理中，S成功，F失败 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `ERROR_CODE` | varchar(64) | 错误编码 · 可空 |
| `ERROR_MSG` | varchar(256) | 错误信息 · 可空 |

## 主键 / 索引
- 主键:`CTL_VOUCHER_NO`
- `IDX_FUND_CTL_ORDER_RNO`:REL_CTL_VOUCHER_NO
- `IDX_TFCO_GMTCRT`:GMT_CREATE

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

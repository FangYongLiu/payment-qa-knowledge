---
title: PayBy产品类型清单
domain: merchant-portal
kind: wiki_page
slug: payby-api-product-catalog
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p7
tags: []
---

# PayBy产品类型清单

本页列出 PayBy 当前对接支持的产品类型（product）及其适用场景说明，供商户在接入时根据业务形态选择对应产品。相关接口报文中的通用字段定义见 [[payby-api-common-data-structures-part7]]。

## 产品类型一览

| 产品名称 | 产品说明 |
| --- | --- |
| Basic Payment Gateway | 使用包括 JSAPI、APP、PAYPAGE、DYNQR 等场景的产品 |
| Smart Purchase | 使用智能 POS、小白盒等设备完成收款的产品 |
| QRPay | 使用扫码枪等设备扫描用户付款二维码支付的产品 |
| Transfer | 转账到 PayBy 账户的产品 |
| Transfer to bank | 转账到银行卡的产品 |
| InApp | 使用包括 InApp 等场景的产品 |
| Auto Debit | 使用授权协议号支付的产品 |
| Cash Top Up | 使用现金付款完成线上订单支付的产品 |

## 分类说明

- **线上收银场景**
  - Basic Payment Gateway：覆盖 JSAPI、APP、PAYPAGE、DYNQR 等多种线上接入形态。
  - InApp：用于 InApp 等应用内支付场景。
- **线下收银场景**
  - Smart Purchase：基于智能 POS、小白盒等硬件设备完成收款。
  - QRPay：通过扫码枪等设备扫描用户出示的付款二维码完成支付。
- **转账类产品**
  - Transfer：资金转入 PayBy 账户。
  - Transfer to bank：资金转入银行卡。
- **协议/现金类产品**
  - Auto Debit：基于授权协议号发起代扣支付。
  - Cash Top Up：用户以现金方式完成线上订单支付。

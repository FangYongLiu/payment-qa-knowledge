---
title: 费率配置与策略库常用表
domain: payment-database-reference
kind: wiki_page
slug: pricing-database-tables
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:79d1eee0-a479-47fd-8b3d-ec12172156f3
tags: []
---

# 费率配置与策略库常用表

本页汇总 `ppcenter`（产品模板、费率定义、产品申请与产品包）与 `pbsdb`（费率策略与价格计算）两个库中常用表，用于费率配置与定价策略相关查询。相关交易侧表见 [[trade-statement-database-tables]]，全库速查见 [[common-database-tables-guide]]。

## ppcenter 费率配置

围绕"产品模板 → 费率定义 → 费率配置 → 产品申请 → 产品包"链路：

- `t_product_template`：产品模板
- `t_calculation_define`：费率定义
- `t_price_cal`：费率配置
- `t_product_apply_order`：产品申请
- `t_product_apply_info`：申请审核资料
- `t_package_define`：产品包
- `t_package_template_relation`：产品包与产品模板的关联

## pbsdb 费率策略

定价策略与价格计算相关：

- `tb_pbs_price_strategy_unit`：费率策略
- `tb_pbs_price_strategy_param`：策略详情
- `tb_pbs_price_cal`：价格计算策略

## 相关链接

- 商户与设备：[[merchant-device-database-tables]]
- 会员与账户：[[member-database-tables]]
- 交易与账单：[[trade-statement-database-tables]]

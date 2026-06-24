---
id: svc_transfer
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp053
name: transfer
dev_owner: Guoyou.Ma
aliases: [gp053_transfer]
related_services: []
related_tables: []
---

# transfer

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp053` · domain=`payment-tools`。

## 作用
transfer  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-tools`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
push-to-pay

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_transfer_calculate_fundout]] 出款试算接口、[[api_payby_place_transfer_to_bank_card]] 单笔转账到银行卡接口(placeTransferToBankCard)、[[api_payby_place_transfer_to_bank_order]] 创建单笔付款到银行卡订单、[[api_transfer_place_to_bank_order]] 单笔付款到银行卡下单接口、[[api_transfer_get_fundout_ability_list]] 查询出款能力接口、[[api_payby_get_transfer_to_bank_order]] 查询单笔付款到银行卡订单、[[api_payby_get_transfer_to_bank_card]] 查询转账银行卡接口、[[api_transfer_place_transfer_order]] 单笔付款到账户接口 (placeTransferOrder)、[[api_payby_transfer_get_order]] 查询单笔付款到账户订单接口、[[api_payby_transfer_bank_card_notify]] 商户转账银行卡成功通知、[[api_transfer_get_iban_holder_name]] 查询IBAN姓名接口、[[api_transfer_order_notify]] 商户付款到账户成功通知 (transferOrder Notify)、[[api_transfer_place_transfer_to_bank_order]] 出款到银行卡接口、[[api_payby_transfer_get_iban_holder_name]] 查询IBAN姓名接口、[[api_transfer_get_transfer_order]] 查询单笔付款到账户订单接口 (getTransferOrder)、[[api_payby_transfer_get_fundout_ability_list]] 查询出款能力接口、[[api_payby_transfer_to_bank_notify]] 商户付款到银行卡成功通知

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）

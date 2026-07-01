---
id: scn_offline_merchant_scan_payment_code
object_type: Scenario
name: 商户扫用户付款码线下收单(POS / 扫码枪)
aliases:
- 付款码被POS机扫场景
- 付款码被扫码枪扫场景
- payment code scanned by pos
- payment code scanned by scanner
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289143
tags:
- 线下收单
- 付款码
- POS
- 扫码枪
related_services: [svc_pos_gateway, svc_sgs]
related_tables: []
related_logs: []
---

# 商户扫用户付款码线下收单(POS / 扫码枪)

## 触发 / 入口
用户结账时向商户出示付款码，商户用扫码设备扫描该付款码以发起线下收单交易(主扫商户、被扫用户)。按商户使用的扫码设备分两条子路径:
1. **Smart POS 扫码**:商户用 Smart POS 内置扫码能力扫付款码，POS 直接进入收单交易流程。
2. **扫码枪扫码**:商户用扫码枪等外接扫码设备扫付款码并解析，由商户后端调用 SGS 下单接口发起收单。

## 关联关系
- **涉及服务**:[[svc_pos_gateway]](Smart POS 扫码路径的 POS 流量入口)、[[svc_sgs]](扫码枪路径下商户后端调用的下单服务)(= `related_services`)。
- **校验的表**:待补(原文未提供落库表)。
- **相关流程**:设备前置开通见 [[flow_device_activation]];POS 机型能力差异见 [[scn_offline_pos_device_types]];POS 交易落库校验见 [[scn_pos_transaction_db_check]]。

## 前置条件
- 用户已生成可用的付款码并展示。
- 商户具备扫码设备:Smart POS(内置扫码)或扫码枪等外接扫码设备。
- 扫码枪路径:商户后端可调用 SGS 下单接口。

## 操作步骤
1. 用户出示付款码。
2. 商户扫描用户付款码并解析:
   - Smart POS 子路径:用 Smart POS 扫描付款码，POS 进入收单交易流程。
   - 扫码枪子路径:用扫码枪扫描并解析付款码，商户后端调用 SGS 下单接口发起收单。
3. 收单交易按对应路径完成。

## DB 校验点
- 待补(原文未提供;落库校验可参照 [[scn_pos_transaction_db_check]])。

## 预期结果
- Smart POS 路径:线下收单交易按 Smart POS 扫付款码方式完成。
- 扫码枪路径:通过 SGS 下单接口完成线下收单交易。

> 说明:原文交易流程图未能下载，详细链路细节标「待补」，留待人工补充更新。

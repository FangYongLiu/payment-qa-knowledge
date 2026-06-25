---
id: scn_offline_pos_device_types
object_type: Scenario
name: POS设备机型能力差异校验
aliases:
- POS设备类型
- POS机型清单
- pos device types
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1135378560
tags:
- POS
- 机型
- 能力矩阵
- 回归
related_services: [svc_pos_gateway, svc_offline_payment]
related_tables: []
related_logs: []
---

# POS设备机型能力差异校验

## 触发 / 入口
PayBy POS 业务覆盖多种设备形态与商户场景。对任一机型做交易/开通回归时，需按机型核验其支持的支付方式、硬件能力与资金流差异。本场景是机型回归的能力基线(capability matrix)。

## 关联关系
- **涉及服务**:[[svc_pos_gateway]](POS 流量入口)、[[svc_offline_payment]](线下支付编排)(= `related_services`)。
- **校验的表**:待补(机型差异主要体现在能力/配置，落库校验见 [[scn_pos_transaction_db_check]])。
- **相关流程**:设备开通见 [[flow_device_activation]]。

## 设备机型与能力矩阵
PayBy 现有 6 类 POS 形态，覆盖自营收单、ADCB 合作、出租车场景、虚拟终端等;不同形态在资金流、支付方式、硬件能力上存在差异。

| 设备类型 | 刷卡 | 扫码 | PayLink | 打印 | 资金流 | 说明 |
| --- | --- | --- | --- | --- | --- | --- |
| PayBy POS | ✓ | ✓ | ✓ | 待补 | 有 | 公司自营 POS 机 |
| Smart POS | — | ✓ | ✓ | 待补 | 有 | 公司自营 POS 机(不支持刷卡) |
| Virtual POS | — | ✓ | ✓ | — | 有 | 装在安卓手机上的虚拟终端 |
| ADCB Taxi POS(P2 Mini) | — | — | — | 无 | 无 | 阿布扎比出租车，无打印设备 |
| ADCB Standard POS | — | — | — | 待补 | 无 | ADCB 商户使用 |

> 表中「—」表示该机型不支持/不适用，「待补」表示原文未明确。
> **ADCB POS 系列**(Taxi / Standard)为 ADCB 定制，**无资金流，不涉及资金结算与对账**，兼容两种类型设备;与 PayBy POS / Smart POS 的资金链路需严格区分。

## 通用接入流程
所有设备类型均涉及以下环节(回归须覆盖):
1. 设备激活(通用，详见 [[flow_device_activation]])
2. 密钥注入
3. 产品开通
4. 渠道报备
5. 做交易

## 前置条件
- 已确定待测机型及其归属商户(自营 / ADCB)。

## 操作步骤
1. 按机型确认其支持的支付方式(刷卡/扫码/PayLink)与硬件能力(是否带打印)。
2. 走通用接入流程(激活 → 密钥注入 → 产品开通 → 渠道报备 → 交易)。
3. 对有资金流机型校验结算/对账;ADCB POS 系列确认无资金结算与对账链路。

## DB 校验点
- 有资金流机型的交易落库与结算见 [[scn_pos_transaction_db_check]]。
- ADCB POS 系列不应产生资金结算/对账记录(待补:具体表与断言)。

## 预期结果
- 各机型的支付能力、硬件能力、资金流表现与能力矩阵一致;ADCB POS 系列无资金流。

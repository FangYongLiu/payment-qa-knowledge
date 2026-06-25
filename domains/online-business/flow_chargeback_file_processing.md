---
id: flow_chargeback_file_processing
object_type: Flow
name: Chargeback拒付文件处理端到端流程
aliases: [拒付文件处理, chargeback-process-overview, chargeback文件处理]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/wiki/chargeback/chargeback-process-overview.md
tags: [chargeback, 拒付, file-processing, matching, 对账]
related_services: []
related_tables: [tbl_cmf_tt_inst_order, tbl_grc_t_payment_event]
related_scenarios: [scn_online_business_chargeback_file_intake]
---

# Chargeback拒付文件处理端到端流程

## 概述
将多渠道（VISA、MASTERCARD、MAGNATI、CKO-HISTORY）下发的拒付原始文件，从上传开始解析、检查、结构化入库，并通过多维匹配链路关联到系统内已有的原始交易与清算数据。起点为「用户上传渠道拒付文件」，终点为「chargeback 模型与交易/清算数据完成有效性匹配补全」。

## 步骤(跨系统)

### 1. 上传文件
- 支持的文件类型：`VISA`、`MASTERCARD`、`MAGNATI`、`CKO-HISTORY`。
- 用户选择对应文件类型并上传，按文件类型适配对应渠道。

### 2. 解析文件
- 根据文件类型获取对应的处理器（handler）。
- 解析原始文件，生成对应的文件模型集合。

### 3. 检查数据是否存在
- 通过 `ARN` 检查数据是否已存在。
- 已存在数据：更新状态；具体更新内容由对应处理器判断（各渠道处理器差异化）。

### 4. 数据结构化
- 将文件模型数据转换成 chargeback 模型。
- chargeback 模型的 `valid` 字段初始置为 `0`（待匹配成功后再流转）。

### 5. 数据有效性匹配链路
通过多种匹配键依次校验存在性并补全交易数据：

- **通过 instOrderNo 匹配**
  - `cmf.tt_inst_order`：确认订单是否存在。
  - `grc.t_payment_event`：补充交易数据。
- **通过 arn 匹配**
  - `reconciliation.t_clear_flow`：确认清算流水是否存在（表对象「待补」）。
  - `cmf.tt_inst_order`：获取支付订单号。
  - `grc.t_payment_event`：补充交易数据。
- **通过 authCode 匹配**
  - `reconciliation.t_clear_flow`：确认是否存在 `inst_seq_no`（表对象「待补」）。
  - `cmf.tt_inst_order`：获取支付订单号。
  - `grc.t_payment_event`：补充交易数据。
- **通过 arn 匹配（清算项）**
  - `mchtsettle.t_clearing_item`：检查清算项是否存在（表对象「待补」）。

## 关联关系
- **经过的服务(有序)**：待补（拒付文件处理服务/对账服务尚未建对象；清算流水关联 `payment-core` 域的 `reconciliation` 服务，结算项关联商户结算，待补对象后再连边）。
- **关键表**：[[tbl_cmf_tt_inst_order]]、[[tbl_grc_t_payment_event]]（= `related_tables`）；`reconciliation.t_clear_flow`、`mchtsettle.t_clearing_item`（表对象「待补」）。
- **关键场景**：[[scn_online_business_chargeback_file_intake]]（= `related_scenarios`）。

## 校验点
- 文件类型必须在支持范围（VISA/MASTERCARD/MAGNATI/CKO-HISTORY）内，并能取到对应处理器。
- 通过 `ARN` 判断数据是否已存在；已存在则按处理器规则更新状态/内容（重复 ARN 重传需保证幂等）。
- 结构化后 chargeback 模型 `valid` 初始值为 `0`，匹配成功后状态正确流转。
- 多链路匹配（instOrderNo / arn / authCode）的优先级、互斥/兜底关系正确。
- 跨表匹配链路（cmf.tt_inst_order、grc.t_payment_event、reconciliation.t_clear_flow、mchtsettle.t_clearing_item）数据一致性。
- authCode 匹配中 `inst_seq_no` 的获取与支付订单号关联链路完整。

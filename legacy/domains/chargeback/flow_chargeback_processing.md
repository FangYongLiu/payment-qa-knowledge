---
id: flow_chargeback_processing
object_type: Flow
domain: chargeback
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:4ad39c53-fb2e-43b6-bfb5-310fd4ae19d7
tags:
- chargeback
- file-processing
- matching
subdomain: null
module: null
sensitivity: normal
name: Chargeback文件处理端到端流程
aliases: []
related_services: []
related_tables:
- cmf.tt_inst_order
- grc.t_payment_event
- reconciliation.t_clear_flow
- mchtsettle.t_clearing_item
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Chargeback 文件从上传到结构化入库及数据有效性匹配的端到端处理流程。涵盖文件上传、解析、数据存在性检查、结构化转换，以及通过 instOrderNo / arn / authCode 多链路与交易数据匹配补全。

## 步骤(跨系统)

### 1. 上传文件
- 支持文件类型：VISA、MASTERCARD、MAGNATI、CKO-HISTORY
- 用户选择对应文件上传

### 2. 解析文件
- 根据文件类型获取对应的处理器
- 解析原始文件
- 生成对应的文件模型集合

### 3. 检查数据是否存在
- 通过 ARN 检查
- 已存在数据：更新状态，需根据对应的处理器判断更新内容

### 4. 数据结构化
- 将对应的文件模型数据转换成 chargeback 模型
- chargeback 模型 `valid` 设置为 `0`

### 5. 数据有效性匹配链路
- **通过 instOrderNo 匹配**
  - `cmf.tt_inst_order` 确认是否存在
  - `grc.t_payment_event` 补充交易数据
- **通过 arn 匹配**
  - `reconciliation.t_clear_flow` 确认是否存在
  - `cmf.tt_inst_order` 获取支付订单号
  - `grc.t_payment_event` 补充交易数据
- **通过 authCode 匹配**
  - `reconciliation.t_clear_flow` 确认是否存在 `inst_seq_no`
  - `cmf.tt_inst_order` 获取支付订单号
  - `grc.t_payment_event` 补充交易数据
- **通过 arn 匹配（清算项）**
  - `mchtsettle.t_clearing_item` 检查是否存在

## 涉及服务/表
- `cmf.tt_inst_order`：确认订单存在/获取支付订单号
- `grc.t_payment_event`：补充交易数据
- `reconciliation.t_clear_flow`：确认清算流水存在 / `inst_seq_no`
- `mchtsettle.t_clearing_item`：清算项存在性检查

## 校验点
- 文件类型必须匹配支持范围（VISA/MASTERCARD/MAGNATI/CKO-HISTORY），并取到对应处理器
- 通过 ARN 判断数据是否已存在；已存在则按处理器规则更新状态/内容
- 结构化后 chargeback 模型 `valid` 初始值为 `0`
- 多链路匹配（instOrderNo / arn / authCode）用于确认数据存在性并补全交易数据

</result>

---
id: domain_chargeback
object_type: Domain
domain: chargeback
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:4ad39c53-fb2e-43b6-bfb5-310fd4ae19d7
tags:
- chargeback
- 拒付
- 对账
subdomain: null
module: null
sensitivity: normal
name: Chargeback业务域
aliases: []
related_services: []
related_tables:
- cmf.tt_inst_order
- grc.t_payment_event
- reconciliation.t_clear_flow
- mchtsettle.t_clearing_item
related_scenarios:
- chargeback-process-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Chargeback业务域负责处理来自多渠道（VISA、MASTERCARD、MAGNATI、CKO-HISTORY）的拒付文件，覆盖文件上传、解析、数据检查、结构化以及数据有效性匹配的端到端链路。核心目标是将外部渠道下发的拒付原始文件转化为系统内部统一的 chargeback 模型，并通过多种匹配维度关联到原始交易与清算数据。

## 覆盖范围
- 拒付文件类型：VISA、MASTERCARD、MAGNATI、CKO-HISTORY
- 文件上传与渠道适配
- 文件解析与模型集合生成
- 通过 ARN 进行数据存在性检查与状态更新
- 文件模型到 chargeback 模型的结构化转换（valid 默认置为 0）
- 数据有效性匹配链路（instOrderNo / arn / authCode 多维匹配）
- 关联表：cmf.tt_inst_order、grc.t_payment_event、reconciliation.t_clear_flow、mchtsettle.t_clearing_item

## 关键服务/流程
Chargeback流程包含 7 个主要阶段（参考 [[flow_chargeback_processing]]、[[chargeback-process-overview]]）：

1. **上传文件**：根据文件类型（VISA/MASTERCARD/MAGNATI/CKO-HISTORY）选择对应渠道上传。
2. **解析文件**：按文件类型获取对应处理器，解析原始文件，生成文件模型集合。
3. **检查数据是否存在**：通过 ARN 检查；若已存在数据则更新状态，更新内容由对应处理器决定。
4. **数据结构化**：将文件模型数据转换为 chargeback 模型，chargeback 模型 valid 字段设置为 0。
5. **数据有效性匹配链路**：
   - 通过 **instOrderNo** 匹配：cmf.tt_inst_order 确认是否存在；grc.t_payment_event 补充交易数据。
   - 通过 **arn** 匹配：reconciliation.t_clear_flow 确认是否存在；cmf.tt_inst_order 获取支付订单号；grc.t_payment_event 补充交易数据。
   - 通过 **authCode** 匹配：reconciliation.t_clear_flow 确认是否存在 inst_seq_no；cmf.tt_inst_order 获取支付订单号；grc.t_payment_event 补充交易数据。
   - 通过 **arn** 匹配：mchtsettle.t_clearing_item 检查是否存在。

## QA 关注点
- 各渠道（VISA/MASTERCARD/MAGNATI/CKO-HISTORY）文件解析处理器是否正确路由与覆盖
- ARN 存在性检查时，更新状态逻辑是否依处理器差异化处理正确
- chargeback 模型 valid 初始值是否为 0，以及后续匹配成功后的状态流转
- 多匹配维度（instOrderNo / arn / authCode）的优先级与互斥/兜底关系
- 跨表匹配链路（cmf.tt_inst_order、grc.t_payment_event、reconciliation.t_clear_flow、mchtsettle.t_clearing_item）数据一致性
- 重复 ARN 文件重传场景下的幂等性与状态更新正确性
- authCode 匹配中 inst_seq_no 的获取与支付订单号关联链路完整性

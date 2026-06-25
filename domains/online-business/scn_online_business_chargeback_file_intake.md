---
id: scn_online_business_chargeback_file_intake
object_type: Scenario
name: Chargeback拒付文件上传与匹配场景
aliases: [拒付文件上传匹配, chargeback文件入库]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/domains/chargeback/domain_chargeback.md
tags: [chargeback, 拒付, file-processing, matching]
related_services: []
related_tables: [tbl_cmf_tt_inst_order, tbl_grc_t_payment_event]
related_logs: []
---

# Chargeback拒付文件上传与匹配场景

## 触发 / 入口
- 入口操作：用户上传渠道拒付文件（VISA / MASTERCARD / MAGNATI / CKO-HISTORY）。
- 端到端流程见 [[flow_chargeback_file_processing]]。

## 关联关系
- **涉及服务**：待补（拒付文件处理 / 对账服务对象尚未建立）。
- **校验的表**：[[tbl_cmf_tt_inst_order]]、[[tbl_grc_t_payment_event]]（= `related_tables`）；`reconciliation.t_clear_flow`、`mchtsettle.t_clearing_item`（对象「待补」）。
- **相关日志**：待补。
- **测它的接口**：待补（拒付文件上传/解析 API 对象尚未建立）。
- **覆盖它的自动化**：待补。

## 前置条件
- 已有原始交易与清算数据可供匹配：`cmf.tt_inst_order` 有订单、`grc.t_payment_event` 有交易事件、`reconciliation.t_clear_flow` 有清算流水。
- 上传的文件类型在支持范围内并能取到对应处理器。

## 操作步骤
1. 选择文件类型并上传对应渠道的拒付文件。
2. 系统按文件类型路由到对应处理器解析，生成文件模型集合。
3. 通过 `ARN` 检查数据是否已存在；已存在则按处理器规则更新状态。
4. 将文件模型结构化为 chargeback 模型，`valid` 初始置为 `0`。
5. 依次走 instOrderNo / arn / authCode 多链路匹配，补全交易数据并校验存在性。

## DB 校验点
- `cmf.tt_inst_order`：instOrderNo / arn 匹配确认订单存在，并获取支付订单号。
- `grc.t_payment_event`：补全交易数据。
- `reconciliation.t_clear_flow`：arn / authCode 匹配确认清算流水存在、取 `inst_seq_no`（表对象待补）。
- `mchtsettle.t_clearing_item`：arn 匹配确认清算项存在（表对象待补）。
- chargeback 模型 `valid` 字段初始为 `0`，匹配成功后状态流转是否正确。

## 预期结果
- 各渠道文件被正确路由到对应处理器并完整解析。
- 重复 ARN 文件重传时具备幂等性，状态更新正确。
- chargeback 模型经多链路匹配后正确关联到原始交易/清算数据并完成有效性流转。

## QA 关注点
- 各渠道（VISA/MASTERCARD/MAGNATI/CKO-HISTORY）处理器路由与覆盖是否正确。
- ARN 存在性检查时差异化更新逻辑是否正确。
- 多匹配维度（instOrderNo / arn / authCode）优先级与互斥/兜底关系。
- 跨表匹配链路数据一致性。
> 不确定 / 缺失的点已标「待补」，留待人工补充。

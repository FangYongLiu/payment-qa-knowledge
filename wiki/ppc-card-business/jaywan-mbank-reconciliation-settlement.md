---
title: Jaywan mBank Botim卡 - 对账与结算流程
domain: ppc-card-business
kind: wiki_page
slug: jaywan-mbank-reconciliation-settlement
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:c35b0d12-9994-4698-ad4e-538e1511baa7
tags: []
---

# Jaywan mBank Botim卡 - 对账与结算流程

本页汇总 Jaywan mBank Botim 卡项目的对账文件交付方式、结算周期与切分时间，以及退款/取消/拒付在文件中的呈现方式与差异处理原则。

## 对账文件交付与格式

- **交付方式**：属于开发范围，目前 mBank 主机端仅有界面；mBank 现行做法是用 switch 文件与 CBUAE 做对账。具体 SFTP/API/邮件方式待开发确定。
- **文件格式**：当前 mBank 使用 Excel 格式的对账文件，将为 Astratech 定制；可先共享现有 mBank recon 文件格式作参考。
- **频率**：T+1 提供，具体时间待定；频率视交易量而定（daily 或 batch-based）。
- **可定制性**：对账报表是否按 Astratech 需求定制，待进一步讨论。

相关报表清单参见 [[jaywan-mbank-botim-portal-and-reports]]。

## 时区与切分时间

- 交易时间戳统一按 **UAE 时区**。
- 日切时间：**UAE 时间 4 AM**。
- 结算与对账报表均一致沿用该时区。

## 结算周期

- **结算频率**：每天一次，UAE 时间 4 AM。
- **批次数**：每日仅一个批次（once a day）。
- **Cut-off**：UAE 时间 4 AM 接收结算文件。
- **周末与公共假日**：每日结算文件照常生成，但**处理（processing）只在工作日**进行。
- **分账 / 分期结算（split settlement、T+1 部分结算）**：**不支持**。
- **预付资金**：Botim 需提前向 mBank 账户预存资金（pre-funded），用于按时结算。
- **自动扣款**：CBUAE 侧的结算由 mBank 与 mBank Operations 完成，存在自动扣款机制。
- **结算建议（advisement）**：由 mBank Operations（Mahesh）每日提供。

## 文件中的交易类型呈现

- 单个对账文件中包含的交易类型（分项展示）：
  - 购买（purchases）
  - 退款（refunds）
  - 取消（cancellations）
  - 拒绝交易（declined transactions）
- **Chargebacks**：在同一文件内**单独分项展示**（shown separately），不另出单独文件；费用（Fee）也合并在同一文件中，无单独文件。详见 [[jaywan-mbank-fees-chargeback-uat]] 与 [[domain_chargeback]]。

## 退款与取消的体现

- 退款和取消均通过 settlement file 下发，与原交易在**同一个结算文件**中分项展示。
- **退款与原交易的关联**：取决于 acquirer
  - 可能带原交易 reference，也可能不带；
  - 若无 reference，退款将以**贷记交易（credit transaction）**形式出现，不与原始交易做关联。
- 退款发生时，**IRF（Interchange Reimbursement Fee）会被回收（debit）** 到 mBank/Botim，并征收 processing fee（费用细节见 [[jaywan-mbank-fees-chargeback-uat]]）。

## 结算差异与延迟处理

- **结算差异（金额/笔数不一致）**：处理机制待 mBank 进一步明确（原文未给出具体流程）。
- **延迟结算罚则**：通过 Botim **预存资金到 mBank 账户**的方式规避，未单列罚金条款。

## 测试与样例文件

- mBank 可共享现行 recon 文件格式作为参考样例；UAT 环境与 sample 文件相关安排见 [[jaywan-mbank-fees-chargeback-uat]]。

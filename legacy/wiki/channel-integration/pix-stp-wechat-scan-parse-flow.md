---
title: Pix STP-Wechat 扫码解析流程
domain: channel-integration
kind: wiki_page
slug: pix-stp-wechat-scan-parse-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e02c7fa5-0bdf-4113-98a7-9a34a2b301b1
tags: []
---

# Pix STP-Wechat 扫码解析流程

本页描述 WeChat 钱包扫描 Pix 二维码后，经由 cgs 调用 pix，并由 pix 向 Tenpay 查询商户信息，最终在钱包侧展示商户信息的端到端时序。

## 参与方

- User：发起扫码的用户
- Wallet：WeChat 钱包端
- cgs：渠道网关服务
- pix：Pix 业务服务（流程焦点）
- vendor(Tenpay)：外部供应商，提供商户码查询能力

## 时序步骤

1. **scan**：User → Wallet，用户在钱包内扫描 Pix 二维码。
2. **get-rules**：Wallet → cgs，调用 `/pix/mpc/v1/get-rules` 获取解析规则；cgs 内部转发至 pix。
3. **match rule**：Wallet 本地根据规则匹配扫描得到的二维码内容。
4. **parse**：Wallet → cgs，调用 `/pix/mpc/v1/parse` 进行解析；cgs 内部再次转发至 pix。
5. **query merchant code**：pix → vendor(Tenpay)，向 Tenpay 查询商户码。
6. **show merchant information**：Wallet 本地渲染商户信息。
7. **返回**：Wallet → User（虚线返回），向用户展示商户信息。

## 关键说明

- 规则获取与解析分两次调用，先 `get-rules` 再 `parse`，规则匹配在 Wallet 本地完成。
- cgs 作为网关，对 `get-rules` 与 `parse` 两个接口均委派给 pix 处理。
- 商户信息的权威来源为 vendor(Tenpay)，由 pix 在 `parse` 阶段同步查询。
- pix 为本流程的核心服务（时序图中以橙色高亮其活动期）。

## 接口一览

- `/pix/mpc/v1/get-rules`：获取 Pix 二维码解析规则
- `/pix/mpc/v1/parse`：解析 Pix 二维码并返回商户信息

---
title: PIX-Wechat(Tenpay)对账文件流程
domain: channel-integration
kind: wiki_page
slug: pix-wechat-reconciliation-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b22f9f17-3139-4aa3-848a-b041eabc2232
tags: []
---

# PIX-Wechat(Tenpay)对账文件流程

本页描述 PIX 组件作为中心协调者，串联 Tenpay 渠道与 UFS 存储完成对账文件下载与自动对账的时序流程。

## 参与方

- **Time**：定时触发方（actor）
- **reconciliation**：对账组件
- **pix**：中心协调组件（在两个流程中均被激活，承担调度职责）
- **ufs**：文件存储
- **vendor (Tenpay)**：Wechat/Tenpay 渠道

## 流程 1：下载对账文件 (download check file)

由 Time 触发到 pix：

- **1**: download check file — Time → pix
  - **1.1**: get file address — pix → vendor (Tenpay)
  - **1.2**: upload — pix → ufs

pix 先向 Tenpay 获取对账文件地址，随后上传至 UFS。

## 流程 2：自动对账 (auto reconciliate)

由 Time 触发到 reconciliation：

- **2**: auto reconciliate — Time → reconciliation
  - **2.1**: get file — reconciliation → pix
    - **2.1.1**: get file content — pix → ufs

reconciliation 通过 pix 获取文件，pix 再从 UFS 读取文件内容。

## 关键说明

- pix 在两个流程中均为核心编排者，居中对接 vendor (Tenpay) 与 ufs。
- 文件下载与自动对账解耦：先由流程 1 把文件落地 UFS，流程 2 再从 UFS 读取消费。
- 调用均为同步调用（实线箭头 + 实心三角）。

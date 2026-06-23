---
title: Pix退款交易状态机
domain: acquire-transaction
kind: wiki_page
slug: pix-refund-state-diagram
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:4fd779b5-b452-48a1-bf55-8c59fa690f83
tags: []
---

# Pix退款交易状态机

描述 Pix 退款交易从发起到终态的生命周期，包含 Processing、WaitRetry、Success、Fail 四个状态及其流转触发条件。

## 状态列表

- **P-Processing**：退款处理中（中间态）
- **WR-WaitRetry**：退款失败后等待重试（中间态）
- **S-Success**：退款成功（终态）
- **F-Fail**：退款失败（终态）

## 初始流转

退款发起后，根据校验结果分为两条路径：

- `validation fail` → **F-Fail**：校验失败，直接进入失败终态
- `refund initiated` → **P-Processing**：校验通过，进入处理中

## Processing 后续流转

从 **P-Processing** 出发：

- `refund success` → **S-Success**：退款成功，进入成功终态
- `refund fail` → **WR-WaitRetry**：退款失败，进入等待重试

## WaitRetry 流转

从 **WR-WaitRetry** 出发：

- `retry` → **P-Processing**：触发重试，回到处理中状态

## 终态

- **F-Fail**：失败终态（来自校验失败）
- **S-Success**：成功终态（来自 Processing 退款成功）

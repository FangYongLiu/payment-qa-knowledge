---
title: POS离线支付系统架构图
domain: device-pos
kind: wiki_page
slug: pos-offline-payment-architecture
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9c712a85-1ff1-46a9-9735-f1e87cb0d541
tags: []
---

# POS离线支付系统架构图

本页描述 POS 离线支付系统从终端到渠道层的分层组件架构与依赖关系（UML 组件图 "cmp 组件图"）。

## 分层结构

自上而下分为四层：

- **网关层**
- **应用层**
- **中台**
- **渠道层**

外部系统包括：`pos terminal`、`ni-sftp`、`ni-server`；其余为内部组件。

## 组件与层级归属

### 终端（外部）
- `pos terminal`：POS 终端入口。

### 网关层
- `pos-gateway`：接收来自 `pos terminal` 的请求，链路协议为 `https iso8583`。

### 应用层
- `收单`：由 `pos-gateway` 经 `dubbo iso8583` 调用。

### 中台
- `pfs/dpm`
- `offline-payment`：依赖 `pfs/dpm`（虚线依赖）。

### 渠道层
- `counter`
- `qpay-nipos`：依赖 `hsm`（虚线依赖）。
- `nisocket`：由 `qpay-nipos` 连接。
- `hsm`

## 依赖与调用链路

- `pos terminal` → `pos-gateway`（`https iso8583`）
- `pos-gateway` → `收单`（`dubbo iso8583`）
- `收单` → 中台（`pfs/dpm`、`offline-payment`）
- `offline-payment` ⇢ `pfs/dpm`（虚线依赖）
- `offline-payment` → 渠道层（`counter`、`qpay-nipos`）
- `qpay-nipos` → `nisocket`
- `qpay-nipos` ⇢ `hsm`（虚线依赖）

## 渠道层对外出口

- `counter` ⇢ `ni-sftp`（虚线依赖，外部系统）
- `nisocket` → `ni-server`（链路 `base24`，外部系统）

## 图例约定

- **青色框**：外部系统（`pos terminal`、`ni-sftp`、`ni-server`）。
- **粉色框**：内部组件。
- **虚线箭头**：依赖关系（dependency）。
- **实线箭头 + 协议标注**：调用链路（如 `https iso8583`、`dubbo iso8583`、`base24`）。

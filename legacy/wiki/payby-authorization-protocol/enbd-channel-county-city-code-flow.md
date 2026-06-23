---
title: ENBD渠道 County/City Code 字段流转
domain: authorization-protocol
kind: wiki_page
slug: enbd-channel-county-city-code-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:580c9f5e-c9b3-496c-a1f6-5e3d218875a1
tags: []
---

# ENBD渠道 County/City Code 字段流转

本页描述 ENBD 渠道下，`Countycode` 与 `citycode` 字段在「商户提现」与「商户转账」两类场景中跨系统的传递路径，以及 CMF 反查 `cityname` 的终点处理。

## 商户提现场景

字段流转链路：

`Portal` → `受益人` → `Fundout` → `CMF`

- **Portal**：录入 `Countycode`、`citycode`
- **受益人**：存储 `Countycode`、`citycode`
- **Fundout**：透传 `Countycode`、`citycode`
- **CMF**：根据 `Citycode` 反查 `cityname`

## 商户转账场景

字段流转链路：

`商户接口` → `Fundout` → `CMF`

- **商户接口**：传入 `Countycode`、`citycode`
- **Fundout**：透传 `Countycode`、`citycode`
- **CMF**：根据 `Citycode` 反查 `cityname`

## 两个场景的差异

- 商户提现的入口为 Portal 录入，并且在 `受益人` 节点会落库存储 `Countycode`、`citycode`。
- 商户转账的入口为商户接口直接传入，链路上没有受益人存储节点。
- 两个场景的终点一致：均由 CMF 通过 `Citycode` 反查 `cityname`。

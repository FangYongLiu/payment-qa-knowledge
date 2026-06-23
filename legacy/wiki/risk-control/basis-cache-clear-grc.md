---
title: Basis后台风控服务缓存清理操作
domain: risk-control
kind: wiki_page
slug: basis-cache-clear-grc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3d0b7742-087f-4318-b17c-0888b5a450d1
tags: []
---

# Basis后台风控服务缓存清理操作

在 Basis 后台通过 Function Query 下的 Cache Clear 入口，可针对 grc 风控相关服务执行缓存清理。

## 入口路径

- 系统：PAYBY BASIS（如 `sim.intra.test2pay.com/basis/`）
- 导航：GENERAL → Function Query → Cache Clear

## 查询方式

- 在 Cache Clear 页面的搜索框输入 `grc`，点击 Search 按钮
- 结果以表格形式展示，列包括 `serviceName`（可排序）与 `Action`

## grc 相关服务列表

搜索 `grc` 后返回 4 条服务记录：

1. `gp079_grc-component-connect-provider` — Action 提供两个按钮：`caffeineCacheManager`、`cacheManager`
2. `gp079_grc-cps-provider`
3. `gp079_grc-engine-provider`
4. `gp079_grc-check-identity-provider`

## 操作说明

- 对 `gp079_grc-component-connect-provider`，可分别点击 `caffeineCacheManager` 或 `cacheManager` 执行对应缓存的清理
- 其余三个 grc 服务在结果中未展示 Action 按钮

## 分页与展示

- 默认每页 10 条（`10 articles/page`），共 4 条（`total of 4 articles`）
- 支持 `skip to page` 输入页码后点击 `confirm` 跳转

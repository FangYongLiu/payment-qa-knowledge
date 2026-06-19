---
id: tbl_fiserv_out_bound
object_type: Table
domain: authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2199912473
tags:
- fiserv
- tid
- outbound
subdomain: fiserv
module: device
sensitivity: normal
name: device.t_fiserv_out_bound
aliases: []
related_services: []
related_tables:
- tbl_fiserv_ping_url
related_scenarios:
- scn_fiserv_test_tid_creation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储 Fiserv 通过 sftp 提供的 outbound 文件(原始 .xml)解析后的 TID 数据。PayBy 每天扫描 sftp 文件并解析为 excel 格式后落库到此表。在 basis merchant → TMS → Activated Devices → Fiserv Outbound Files 目录中查看的就是该表的数据。设备绑定渠道 TID 时，需输入此表中状态为 Inactive 的 TID；渠道绑定成功后，对应记录的 config_status 由 INACTIVE 更新为 ACTIVED。

## 关键列
- `config_status`：TID 配置状态，初始解析入库时为 `INACTIVE`，渠道绑定成功后更新为 `ACTIVED`。
- `TID`：终端 ID，必须唯一，不能重复。
- `mid`：商户号，分两种前缀：
  - `1209` 开头：出租车公司
  - `7600` 开头：非出租车公司
- `store_id`：门店 ID，根据 mid 推导：
  - mid 为 `1209` 开头：把 mid 前 2 位替换为 `8116` 作为 store_id
  - mid 为 `7600` 开头：把 mid 前 4 位替换为 `8116` 作为 store_id
- 文件路径：解析来源文件的路径(测试环境构造时不重要)。

## 主键/索引
原文未说明。

## 校验点(QA 关注)
- 新解析入库的记录 `config_status` 应为 `INACTIVE`。
- 同一 TID 不能重复(测试环境手动插入数据时尤其需要保证)。
- `store_id` 的生成规则需与 mid 前缀严格对应(1209→替换前2位为8116；7600→替换前4位为8116)。
- 渠道绑定成功后：
  - 该 TID 在 `device.t_fiserv_out_bound` 中的 `config_status` 更新为 `ACTIVED`
  - `device.t_device_channel` 中应落一条 device_id 与 TID 关联的数据
- basis merchant → TMS → Activated Devices → Fiserv Outbound Files 目录展示的数据应与表内一致。
- 测试环境构造新 TID 时，可手动插入 `config_status='INACTIVE'` 的记录用于后续绑定测试。

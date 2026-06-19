---
id: tbl_fiserv_out_bound
object_type: Table
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:529d83bb-f8c0-47a4-af94-b05017e2e750
tags:
- fiserv
- tms
- tid
subdomain: device
module: fiserv
sensitivity: normal
name: device.t_fiserv_out_bound
aliases: []
related_services: []
related_tables:
- tbl_fiserv_ping_url
related_scenarios:
- scn_fiserv_test_env_mock_tid
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储Fiserv通过sftp提供的outbound文件(原始.xml)解析后的TID数据。PayBy每天扫描sftp文件，解析为excel格式后落库到本表，记录TID及其激活状态。在 basis merchant → TMS → Activated Devices → Fiserv Outbound Files 目录可查看本表中解析到的所有TID数据。

## 关键列
- `config_status`：TID激活状态。新解析入库的数据为 `INACTIVE`；渠道绑定成功后更新为 `ACTIVED`。
- `TID`：Fiserv提供的终端ID，全表内不可重复。
- `mid`：商户ID。两种取值开头：
  - `1209` 开头：出租车公司
  - `7600` 开头：非出租车公司
- `store_id`：根据mid派生：
  - mid以 `1209` 开头：将mid前2位替换为 `8116` 作为 store_id
  - mid以 `7600` 开头：将mid前4位替换为 `8116` 作为 store_id
- 文件路径相关字段：在测试环境插入mock数据时不重要。

## 主键/索引
原文未明确说明。TID在业务上需保持唯一(测试环境插入数据时强调TID不能重复)。

## 校验点(QA 关注)
- 新解析入库的记录 `config_status` 必须为 `INACTIVE`，才会出现在 Fiserv Outbound Files 中作为可绑定的TID。
- 在 basis merchant → TMS → Activated Devices → Device Configuration 绑定时，输入的TID必须是本表中状态为 `Inactive` 的记录。
- 渠道绑定成功后：
  - 本表对应TID记录的 `config_status` 应更新为 `ACTIVED`
  - `device.t_device_channel` 应同步落一条 device_id 与 TID 关联的数据
- 测试环境mock TID时校验：
  - TID不可与已有记录重复
  - mid前缀需为 `1209` 或 `7600`
  - store_id 派生规则需与 mid 前缀对应正确(1209→替换前2位为8116；7600→替换前4位为8116)
  - `config_status` 初始必须为 `INACTIVE`

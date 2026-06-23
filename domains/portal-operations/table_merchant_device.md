---
id: tbl_merchant_device
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- device
- activation
- merchant-binding
subdomain: device-activation
module: null
sensitivity: normal
name: 商户设备关系表
aliases:
- t_merchant_device
- device.t_merchant_device
related_services:
- svc_merchant
---

## 用途

`device.t_merchant_device`（商户设备关系表）用于在设备激活成功后，落地保存**商户-门店-设备号**的三元绑定关系，是设备从「申请 → 硬件入库 → 激活码下发 → 激活绑定 → 功能开通」全链路中的**核心归属关系表**。

该表记录了某台物理设备最终归属于哪个商户、哪个门店，以及对应的业务设备号，是后续 POS 交易、Fiserv 收单交易、结算落库等场景中能够通过设备号回溯商户/门店信息的关键依据。

## 在激活链路中的位置

```
t_device_apply_order(申请单, 状态: CREATED/PASSED/REJECTED/ACTIVE_CODE_CREATED)
        │  审核 PASSED → 生成激活码
        ▼
t_active_code(激活码, 状态: ENABLE/USED)
        │  POS 扫码激活
        ▼
t_hardware_info(硬件信息, 首次激活落库, 含 SN / type)
        │
        ▼
t_merchant_device(商户-门店-设备绑定) ◄── hardware_id = t_hardware_info.id
        │
        ▼
t_device_ext(设备开通功能配置, device_id = t_merchant_device.id)
```

## 关键列

- `id`：主键，被 `t_device_ext.device_id` 引用（`device_id = t_merchant_device.id`），用于挂载设备已开通的功能配置。
- `hardware_id`：关联 `t_hardware_info.id`，指向具体的物理设备硬件信息记录，用于回溯设备 SN、设备类型（type，如 Smart POS）等硬件属性。
- 商户、门店、设备号相关字段：用于表达「商户-门店-设备」的三元绑定关系（原文未列出具体列名，以实际表结构为准）。

## 主键 / 索引

- 主键 `id`：被下游 `t_device_ext.device_id` 引用，作为设备功能配置的挂载点。
- `hardware_id`：与 `t_hardware_info.id` 对应（业务上单台物理设备同一时间应仅有一条有效绑定）。

## 与关联表的关系

| 关联表 | 关联字段 | 关系说明 |
| --- | --- | --- |
| `tbl_device_apply_order` | 商户号 / 门店号 | 申请阶段确定商户/门店归属，激活后应与本表一致 |
| `tbl_hardware_info` | `hardware_id = t_hardware_info.id` | 指向具体物理设备的硬件信息（SN、type） |
| `tbl_active_code` | 通过 `hardware_id` / 设备号 | 激活码状态变为 USED 后触发本表落地 |
| `t_device_ext` | `t_device_ext.device_id = t_merchant_device.id` | 挂载设备功能开通配置 |

## 校验点（QA 关注）

1. **激活后落库**：设备激活成功后，`device.t_merchant_device` 应产生对应记录，且 `hardware_id` 与 `t_hardware_info.id` 一致。
2. **申请-激活一致性**：商户号、门店号、设备号应与申请阶段 `t_device_apply_order` 中信息一致，不应出现张冠李戴。
3. **激活码联动**：本表落库时对应的 `t_active_code` 记录应已变为 `USED` 状态。
4. **下游功能配置可达**：通过 `t_merchant_device.id` 应能在 `t_device_ext` 中查询到对应的设备功能配置记录。
5. **唯一性约束**：同一 `hardware_id`（同一物理设备）的有效绑定关系应唯一，避免重复绑定到多个商户/门店。
6. **链路回溯**：在 POS/Fiserv 交易落库检查（如 TID 构造、销售订单落库）时，应能通过设备号经由本表回溯到商户、门店，保证交易归属正确。

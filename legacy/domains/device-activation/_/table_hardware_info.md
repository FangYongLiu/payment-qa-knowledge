---
id: tbl_hardware_info
object_type: Table
domain: device-pos
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:de4113f2-55a3-48f8-b592-6714684acf4c
tags:
- 设备激活
- 硬件信息
subdomain: null
module: null
sensitivity: normal
name: 设备硬件信息表
aliases:
- t_hardware_info
- device.t_hardware_info
related_services: []
related_tables:
- tbl_active_code
- tbl_device_apply_order
- tbl_merchant_device
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
`device.t_hardware_info` 用于保存设备首次激活后的物理硬件信息。设备扫描激活二维码完成激活后，系统向该表写入一条记录，登记该设备的物理序列号与激活的设备类型，作为该硬件设备在收单体系中的唯一身份锚点。

## 在交易链路中的位置
该表位于「设备申请 → 激活码下发 → 设备激活 → 商户绑定 → POS 交易」链路的「设备激活」节点：

1. 业务方在 `tbl_device_apply_order`（设备申请订单表）中提交设备申请，确定设备类型（如 Smart POS）。
2. 系统在 `tbl_active_code`（设备激活码表）中生成激活码，初始状态为 `ENABLE`。
3. 设备扫描激活二维码完成激活后：
   - `tbl_active_code` 中对应激活码状态由 `ENABLE` 变为 `USED`；
   - `device.t_hardware_info` 新增一条记录，写入物理 SN 与设备类型；
   - `device.t_device_key` 写入该硬件对应的设备公钥；
   - `device.t_merchant_device`（商户设备关系表）建立商户与该硬件的绑定关系。
4. 后续 POS 刷卡交易（如 Fiserv 销售/撤销/退款/Reversal 等）通过商户-设备关系定位到该硬件，作为交易上下文的一部分。

## 关键列
- `id`：主键，被下列表外键引用：
  - `device.t_device_key.id = t_hardware_info.id`（设备公钥）
  - `device.t_merchant_device.hardware_id = t_hardware_info.id`（商户-设备关系）
- `SN`：物理设备序列号，应与实际硬件一致。
- `type`：激活的设备类型，本场景取值为 `Smart POS`，应与申请单 `tbl_device_apply_order` 中的设备类型一致。

## 与关联表的关系
| 关联表 | 关联字段 | 关系说明 |
|---|---|---|
| `tbl_device_apply_order` | 业务侧通过设备类型/申请单串联 | 申请单决定 `type` 取值 |
| `tbl_active_code` | 业务时序联动（同一次激活） | 激活码 `USED` 时本表新增记录 |
| `t_device_key` | `t_device_key.id = t_hardware_info.id` | 1:1，登记设备公钥 |
| `tbl_merchant_device` | `t_merchant_device.hardware_id = t_hardware_info.id` | 1:N，绑定商户与硬件 |

## 校验点 (QA 落库检查要点)
- **新增记录**：设备首次激活成功后，`device.t_hardware_info` 应新增一条记录，且 `SN` 与物理设备序列号一致、`type` 与申请单中的设备类型（Smart POS）一致。
- **外键一致性**：同一次激活动作，`t_hardware_info.id` 应能在 `t_device_key.id` 与 `t_merchant_device.hardware_id` 中关联到对应记录，三者一一对应。
- **激活码联动**：与 `tbl_active_code` 联动校验——激活码状态由 `ENABLE` 变为 `USED` 的同时，`t_hardware_info` 应同步生成对应硬件记录，时间戳应在合理窗口内。
- **与申请单一致**：`type` 应回溯匹配 `tbl_device_apply_order` 中该笔申请的设备类型，避免类型错配。
- **唯一性**：同一物理 `SN` 在正常激活流程下不应出现重复记录（如有重复需排查重复激活/脏数据）。

---
id: tbl_device_t_device_apply_order
object_type: Table
name: 设备申请订单 (t_device_apply_order)
aliases: [t_device_apply_order, device.t_device_apply_order]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: device schema DDL
tags: [offline-business, device]
sensitivity: normal
related_services: []
---

# 设备申请订单 (t_device_apply_order)

## 用途
物理表 `device.t_device_apply_order`,主键 `id`。设备申请订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `merchant_mid` | varchar(50) | 商户mid |
| `ext_apply_id` | varchar(64) | 外部申请id |
| `store_apply_id` | bigint | 门店申请id · 可空 |
| `store_id` | bigint | 门店id · 可空 |
| `apply_number` | int | 申请数量 |
| `apply_type` | varchar(32) | 申请型号 BOX 小白盒 SMART_POS 智能pos |
| `status` | varchar(32) | 状态 CREATED 已创建;  PASSED 已通过; REJECTED 已驳回; ACTIVE_CODE_CREATED 激活码已创建 |
| `applier_mid` | varchar(50) | 申请人会员id |
| `last_audit_history_id` | bigint | 最后审批id · 可空 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_device_t_active_code
object_type: Table
name: 激活码 (t_active_code)
aliases: [t_active_code, device.t_active_code]
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

# 激活码 (t_active_code)

## 用途
物理表 `device.t_active_code`,主键 `id`。激活码。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `apply_id` | bigint | 申请id · 可空 |
| `active_code` | varchar(200) | 激活码 |
| `status` | varchar(32) | 状态 ENABLE 未使用 USED 已使用 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `replacement_info_id` | bigint | Replacement info id · 可空 |
| `active_code_type` | varchar(32) | ActiveCodeType |

## 主键 / 索引
- 主键:`id`
- `uk_active_code`:active_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_device_t_pos_staff
object_type: Table
name: POS员工 (t_pos_staff)
aliases: [t_pos_staff, device.t_pos_staff]
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

# POS员工 (t_pos_staff)

## 用途
物理表 `device.t_pos_staff`,主键 `id`。POS员工。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `merchant_mid` | varchar(50) | 商户id · 可空 |
| `name` | varchar(50) | 名称 |
| `password` | varchar(50) | 密码 |
| `role_id` | bigint | 角色id · 可空 |
| `status` | varchar(32) | 状态 |
| `last_updated_by` | varchar(32) | 最后更新人 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `UDX_PWD_MID`:password, merchant_mid (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

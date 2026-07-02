---
id: tbl_acquireii_t_fiserv_batch
object_type: Table
name: Fiserv 批次表 (t_fiserv_batch)
aliases: [t_fiserv_batch, acquireii.t_fiserv_batch]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# Fiserv 批次表 (t_fiserv_batch)

## 用途
物理表 `acquireii.t_fiserv_batch`,主键 `batch_id`。fiserv批次。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint | 批次ID |
| `device_id` | varchar(32) | 发起方设备id |
| `partner_id` | varchar(32) | partner_id |
| `start_time` | timestamp(3) | 开始时间 |
| `end_time` | timestamp(3) | 结束时间 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`batch_id`
- `uk_fb_device`:device_id (UNIQUE)
- `i_fb_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引,勿混用。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增、防覆盖。
- **device 维度**:按 `device_id` 组织的批次/结算通常唯一,注意重复校验。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。

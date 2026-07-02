---
id: tbl_acquireii_t_wechat_mapping
object_type: Table
name: t_wechat_mapping (t_wechat_mapping)
aliases: [t_wechat_mapping, acquireii.t_wechat_mapping]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, acquireii]
sensitivity: normal
related_services: []
---

# t_wechat_mapping (t_wechat_mapping)

## 用途
物理表 `acquireii.t_wechat_mapping`,主键 `partner_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `partner_id` | varchar(20) | merchant memberId |
| `wechat_mid` | varchar(36) | wechat mid |
| `enable_flag` | varchar(8) | enable flag |
| `mcc` | varchar(12) | wechat mcc |
| `created_time` | timestamp(3) | created time |
| `last_updated_time` | timestamp(3) | update time |
| `data_version` | bigint | 待补 |

## 主键 / 索引
- 主键:`partner_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

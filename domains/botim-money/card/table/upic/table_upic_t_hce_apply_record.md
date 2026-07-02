---
id: tbl_upic_t_hce_apply_record
object_type: Table
name: HCE申请记录 (t_hce_apply_record)
aliases: [t_hce_apply_record, upic.t_hce_apply_record]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# HCE申请记录 (t_hce_apply_record)

## 用途
物理表 `upic.t_hce_apply_record`,主键 `record_id`。HCE申请记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `record_id` | bigint | 记录id：前八后九 |
| `member_id` | varchar(20) | 会员id |
| `device_id` | varchar(64) | 设备id |
| `host_app` | varchar(32) | hostApp |
| `token` | varchar(32) | token |
| `apply_status` | varchar(10) | 申请状态：P=申请中，S=申请成功，F=申请失败 |
| `hce_token` | varchar(32) | hceToken · 可空 |
| `message_id` | varchar(32) | 消息id · 可空 |
| `masked_pan` | varchar(64) | pan掩码 · 可空 |
| `masked_token` | varchar(32) | token掩码 · 可空 |
| `card_face_id` | varchar(32) | 卡面id · 可空 |
| `expire_time` | timestamp | 过期时间 · 可空 |
| `error_message` | varchar(255) | 错误信息 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`record_id`
- `idx_hce_token`:hce_token
- `idx_update_time_member_id`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

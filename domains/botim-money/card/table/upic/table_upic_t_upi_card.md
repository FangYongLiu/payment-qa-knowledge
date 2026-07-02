---
id: tbl_upic_t_upi_card
object_type: Table
name: 银联卡 (t_upi_card)
aliases: [t_upi_card, upic.t_upi_card]
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

# 银联卡 (t_upi_card)

## 用途
物理表 `upic.t_upi_card`,主键 `card_id`。银联卡。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `card_id` | bigint | 卡id：前八后九 |
| `member_id` | varchar(20) | 会员号 |
| `identity_type` | varchar(10) | 证件类型：ID=身份证, PASSPORT=护照 |
| `identity_no` | varchar(32) | 证件号：加密 |
| `mobile_hash` | varchar(64) | 手机号hash |
| `open_device_id` | varchar(64) | 开卡设备 |
| `card_status` | varchar(10) | 状态：OP=OpenProcess, A=Active, DP=DeleteProcess, D=Deleted |
| `token` | varchar(32) | token · 可空 |
| `expire_time` | timestamp | 过期时间 · 可空 |
| `pan` | varchar(128) | pan · 可空 |
| `pan_expiry` | varchar(10) | pan有效期 · 可空 |
| `masked_pan` | varchar(64) | pan掩码 · 可空 |
| `has_pin` | char | Y/N Y已经设置过Pin · 可空 |
| `card_face_id` | varchar(10) | 卡面id · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`card_id`
- `idx_expire_time_status`:expire_time, card_status
- `idx_member_id`:member_id
- `idx_pan`:pan
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

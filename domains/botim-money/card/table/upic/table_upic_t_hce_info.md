---
id: tbl_upic_t_hce_info
object_type: Table
name: HCE信息 (t_hce_info)
aliases: [t_hce_info, upic.t_hce_info]
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

# HCE信息 (t_hce_info)

## 用途
物理表 `upic.t_hce_info`,主键 `info_id`。HCE信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `info_id` | bigint | 信息id：前八后九 |
| `member_id` | varchar(20) | 会员id |
| `device_id` | varchar(64) | 设备id |
| `host_app` | varchar(32) | hostApp |
| `hce_status` | char | hce状态：A=激活，C=关闭 |
| `hce_token` | varchar(32) | hceToken · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`info_id`
- `uk_biz_key`:member_id, device_id, host_app (UNIQUE)
- `idx_hce_token`:hce_token
- `idx_update_time_member_id`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

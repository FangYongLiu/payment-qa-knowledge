---
id: tbl_benefit_t_benefit_notify
object_type: Table
name: t_benefit_notify (t_benefit_notify)
aliases: [t_benefit_notify, benefit.t_benefit_notify]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_benefit_notify (t_benefit_notify)

## 用途
物理表 `benefit.t_benefit_notify`,主键 `notify_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `notify_id` | bigint(11) | 主键 · 可空 |
| `notify_type` | tinyint | 通知类型，1 收益结果通知，2 月度统计通知 |
| `voucher_no` | varchar(64) | 通知凭证号，用来幂等 |
| `member_id` | varchar(32) | 会员id |
| `content` | varchar(255) | 通知内容 · 可空 |
| `notify_status` | char | 通知状态 I：等待通知 P: 通知处理中 S：通知成功 E: 通知处理异常 F 通知失败 · 可空 |
| `notify_time` | timestamp | 通知时间 · 可空 |
| `next_notify_time` | timestamp | 下次通知时间 · 可空 |
| `notify_count` | tinyint(4) | 通知次数 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`notify_id`
- `uk_type_voucher`:voucher_no (UNIQUE)
- `idx_create_time`:create_time, notify_status

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

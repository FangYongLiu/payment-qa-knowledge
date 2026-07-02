---
id: tbl_memberfront_t_change_mobile_record
object_type: Table
name: Mobile number change record (t_change_mobile_record)
aliases: [t_change_mobile_record, memberfront.t_change_mobile_record]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# Mobile number change record (t_change_mobile_record)

## 用途
物理表 `memberfront.t_change_mobile_record`,主键 `id`。Mobile number change record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key |
| `request_no` | varchar(64) | Business request number |
| `member_id` | varchar(20) | Member ID |
| `uid` | varchar(64) | Uid |
| `old_mobile` | varchar(25) | Old mobile number |
| `old_eid` | varchar(25) | Emirates ID bound to the old phone · 可空 |
| `new_mobile` | varchar(25) | New mobile number |
| `change_status` | varchar(15) | Change status: PROCESSING, SUCCESS, FAILED, EXCEPTION |
| `changed_time` | datetime | Actual phone-change completion time, set when status=SUCCESS · 可空 |
| `notify_status` | char | Notify status: Y/N |
| `notify_time` | datetime | Notification sent time · 可空 |
| `device_info` | varchar(255) | Device Info · 可空 |
| `result_msg` | varchar(255) | Result Msg · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | datetime | Create time |
| `update_time` | datetime | Update time |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_uid`:uid
- `uk_request_no`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

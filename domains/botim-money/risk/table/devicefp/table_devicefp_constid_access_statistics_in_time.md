---
id: tbl_devicefp_constid_access_statistics_in_time
object_type: Table
name: constid_access_statistics_in_time (constid_access_statistics_in_time)
aliases: [constid_access_statistics_in_time, devicefp.constid_access_statistics_in_time]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefp schema DDL
tags: [risk, devicefp]
sensitivity: normal
related_services: []
---

# constid_access_statistics_in_time (constid_access_statistics_in_time)

## 用途
物理表 `devicefp.constid_access_statistics_in_time`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `app_key` | varchar(255) | appKey |
| `record_time` | varchar(255) | :"2017-09-11 09:11" |
| `all_count` | int | 待补 |
| `web_count` | int | web |
| `ios_count` | int | iOS |
| `android_count` | int | android |
| `wechat_count` | int | wechat |
| `all_risk_count` | int | 待补 |
| `web_risk_count` | int | web |
| `ios_risk_count` | int | iOS |
| `android_risk_count` | int | Android |
| `wechat_risk_count` | int | wechat |
| `modify_time` | timestamp | 待补 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `un_record_time_and_app_key`:record_time, app_key (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

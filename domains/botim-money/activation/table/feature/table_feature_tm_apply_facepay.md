---
id: tbl_feature_tm_apply_facepay
object_type: Table
name: 开通人脸支付 (tm_apply_facepay)
aliases: [tm_apply_facepay, feature.tm_apply_facepay]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: feature schema DDL
tags: [activation, feature]
sensitivity: normal
related_services: []
---

# 开通人脸支付 (tm_apply_facepay)

## 用途
物理表 `feature.tm_apply_facepay`,主键 `facepay_id`。开通人脸支付。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `facepay_id` | bigint | 主键ID |
| `apply_id` | bigint | 关联流程 |
| `member_id` | varchar(32) | 会员ID |
| `sub_level` | varchar(32) | 会员登记 · 可空 |
| `upload_file` | varchar(32) | 活体大礼包 · 可空 |
| `parse_images` | varchar(512) | 解析得到的图片 · 可空 |
| `status` | varchar(16) | 解析得到的图片 · 可空 |
| `resp_code` | varchar(32) | 响应编码 |
| `resp_msg` | varchar(32) | 响应详细 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`facepay_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

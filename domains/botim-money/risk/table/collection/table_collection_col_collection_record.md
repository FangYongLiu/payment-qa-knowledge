---
id: tbl_collection_col_collection_record
object_type: Table
name: 催收记录表 (col_collection_record)
aliases: [col_collection_record, collection.col_collection_record]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 催收记录表 (col_collection_record)

## 用途
物理表 `collection.col_collection_record`,主键 `id`。催收记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_by` | varchar(100) | 修改人 · 可空 |
| `connect_time` | int | 联系时长 · 可空 |
| `contact_time` | timestamp | 联系时间 |
| `description` | varchar(255) | 备注 · 可空 |
| `is_valid` | tinyint(5) | 是否有效沟通 |
| `member_id` | varchar(50) | 借款人id |
| `method` | int | 联系方式1电话 2totok 3 whatsapp |
| `order_collecton_uid` | varchar(50) | 分案id |
| `bill_no` | varchar(64) | 订单 |
| `promise_repayment_date` | timestamp | 承诺还款时间 · 可空 |
| `result` | tinyint(5) | 联系结果 页面下拉项 · 可空 |
| `status` | tinyint(5) | 状态  是否违规异常等 0初始正常 |
| `target` | varchar(255) | 联系内容 电话号 账号号等 · 可空 |
| `target_type` | int | 联系目标类型 0本人  |
| `user_uid` | varchar(100) | 催收员uid |
| `photo_tags` | varchar(255) | 照片文件tag集合 · 可空 |
| `photo_count` | tinyint | 照片数 · 可空 |
| `type` | tinyint(5) | 类型0 普通 1 orderstatus · 可空 |
| `collection_status` | tinyint(5) | 订单催收状态标签 · 可空 |
| `web_phone_token` | varchar(100) | 每次webphone生成单号 · 可空 |
| `is_answered` | tinyint(5) | 是否接通 |
| `template_uid` | varchar(50) | 关联模版uid · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_contact_time`:contact_time
- `idx_member_id`:member_id
- `idx_order_collecton_uid`:order_collecton_uid
- `idx_user_uid`:user_uid
- `idx_web_phone_token`:web_phone_token

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

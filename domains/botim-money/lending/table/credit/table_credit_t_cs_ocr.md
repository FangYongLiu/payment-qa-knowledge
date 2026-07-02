---
id: tbl_credit_t_cs_ocr
object_type: Table
name: 图片识别 (t_cs_ocr)
aliases: [t_cs_ocr, credit.t_cs_ocr]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 图片识别 (t_cs_ocr)

## 用途
物理表 `credit.t_cs_ocr`,主键 `id`。图片识别。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `id_number` | varchar(50) | eid号码 |
| `name` | varchar(50) | 姓名 英文，空格分隔单词，每个单词的首字母大写，其余字母小写 |
| `nationality` | varchar(50) | 国籍 英文，空格分隔单词，每个单词的首字母大写，其余字母小写 |
| `data_of_birth` | varchar(50) | 出生日期yyyymmdd |
| `expiry_date` | varchar(50) | eid过期日期yyyymmdd · 可空 |
| `gender` | varchar(5) | 性别m男f女 · 可空 |
| `ocr_no` | varchar(64) | ocr no · 可空 |
| `user_id` | varchar(32) | 用户ID · 可空 |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

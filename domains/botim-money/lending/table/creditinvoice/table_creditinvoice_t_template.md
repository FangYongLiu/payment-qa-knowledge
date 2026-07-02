---
id: tbl_creditinvoice_t_template
object_type: Table
name: 模板表 (t_template)
aliases: [t_template, creditinvoice.t_template]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# 模板表 (t_template)

## 用途
物理表 `creditinvoice.t_template`,主键 `id`。模板表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 自增id · 可空 |
| `name` | varchar(128) | 模板名称 |
| `version` | int(64) | 版本 |
| `product_code` | varchar(32) | 产品码 |
| `type` | tinyint | 发票类型，1:放款发票,2:退票tcn,3:还款发票,4:减免tcn,5:展期发票,6:优惠券tcn,7:duedate发票,8:还款退回,10:installmentFee 税退回 |
| `html_content` | text | 模板html内容 |
| `create_time` | timestamp | 入库时间 |

## 主键 / 索引
- 主键:`id`
- `name_version_idx`:name, version (UNIQUE)
- `p_t_v_idx`:product_code, type, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

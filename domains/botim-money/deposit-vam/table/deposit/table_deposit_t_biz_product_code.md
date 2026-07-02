---
id: tbl_deposit_t_biz_product_code
object_type: Table
name: 产品编码表 (t_biz_product_code)
aliases: [t_biz_product_code, deposit.t_biz_product_code]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# 产品编码表 (t_biz_product_code)

## 用途
物理表 `deposit.t_biz_product_code`,主键 `BIZ_PRODUCT_CODE`。产品编码表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BIZ_PRODUCT_CODE` | varchar(32) | 产品编码 |
| `NAME` | varchar(128) | 产品名称 · 可空 |
| `LAB` | varchar(32) | 标签 · 可空 |
| `DESCRIPTION` | varchar(128) | 描述 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`BIZ_PRODUCT_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

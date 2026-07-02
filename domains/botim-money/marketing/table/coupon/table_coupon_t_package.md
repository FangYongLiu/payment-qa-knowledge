---
id: tbl_coupon_t_package
object_type: Table
name: 套餐配置 (t_package)
aliases: [t_package, coupon.t_package]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# 套餐配置 (t_package)

## 用途
物理表 `coupon.t_package`,主键 `package_id`。套餐配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `package_id` | bigint | 主键id |
| `package_code` | varchar(32) | 商品编号 · 可空 |
| `package_name` | varchar(100) | 商品名称 · 可空 |
| `package_category` | varchar(32) | 商品分类 |
| `package_url` | varchar(16) | 商品资源 · 可空 |
| `package_logo` | varchar(32) | 商品图片 · 可空 |
| `package_desc` | varchar(64) | 商品描述 |
| `period` | int (12) | 周期(单位是天) · 可空 |
| `period_algorithm` | varchar(32) | 有效时间周期算法 · 可空 |
| `status` | varchar(3) | 状态（1：下架 2：上架  ） |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`package_id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

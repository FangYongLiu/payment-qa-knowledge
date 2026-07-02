---
id: tbl_bill_t_view_config
object_type: Table
name: 视图配置 (t_view_config)
aliases: [t_view_config, bill.t_view_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bill schema DDL
tags: [payment-core, bill]
sensitivity: normal
related_services: []
---

# 视图配置 (t_view_config)

## 用途
物理表 `bill.t_view_config`,主键 `view_id`。视图配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `view_id` | bigint | 配置ID · 可空 |
| `view_code` | varchar(64) | 视图代码 |
| `biz_product_code` | varchar(10) | 业务产品码 |
| `role` | varchar(32) | 角色 |
| `payment_type` | varchar(32) | 支付类型 |
| `title_expression` | varchar(2000) | 标题表达式 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`view_id`
- `uk_vc_bpc_role_pt`:view_code, biz_product_code, role, payment_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

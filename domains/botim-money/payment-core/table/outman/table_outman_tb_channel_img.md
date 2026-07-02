---
id: tbl_outman_tb_channel_img
object_type: Table
name: 渠道图片表 (tb_channel_img)
aliases: [tb_channel_img, outman.tb_channel_img]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# 渠道图片表 (tb_channel_img)

## 用途
物理表 `outman.tb_channel_img`,主键 `channel_img_id`。渠道图片表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `channel_img_id` | bigint | 主键 |
| `idn` | varchar(30) | 身份证号 |
| `channel_code` | tinyint | 渠道编码：1-ica |
| `img_name` | varchar(150) | 图片名称 |
| `status` | varchar(30) | 认证状态 |
| `resp_code` | varchar(30) | 返回码 |
| `request_id` | varchar(32) | 前置订单号 |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`channel_img_id`
- `idx_idn`:idn

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

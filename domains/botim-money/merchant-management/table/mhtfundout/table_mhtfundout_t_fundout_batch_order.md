---
id: tbl_mhtfundout_t_fundout_batch_order
object_type: Table
name: 批次订单 (t_fundout_batch_order)
aliases: [t_fundout_batch_order, mhtfundout.t_fundout_batch_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# 批次订单 (t_fundout_batch_order)

## 用途
物理表 `mhtfundout.t_fundout_batch_order`,主键 `global_id`。批次订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `voucher_no` | varchar(200) | 凭证号 · 可空 |
| `product_code` | varchar(50) | 产品码 |
| `partner_id` | varchar(50) | 发起方memberId |
| `type` | varchar(50) | 订单类型 |
| `status` | varchar(50) | 状态 |
| `request_time` | timestamp(3) | 商户声明请求时间 |
| `file_id` | varchar(200) | ufs文件id |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `subject` | varchar(200) | 批次标题 · 可空 |
| `currency` | varchar(50) | 币种 · 可空 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_fbo_ct`:created_time
- `i_fbo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

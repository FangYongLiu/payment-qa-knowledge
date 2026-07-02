---
id: tbl_upic_t_batch_open_card
object_type: Table
name: 批量开通卡 (t_batch_open_card)
aliases: [t_batch_open_card, upic.t_batch_open_card]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 批量开通卡 (t_batch_open_card)

## 用途
物理表 `upic.t_batch_open_card`,主键 `data_id`。批量开通卡。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `data_id` | int | 数据ID · 可空 |
| `batch_code` | varchar(32) | 批次 |
| `member_id` | varchar(20) | 会员ID |
| `open_status` | char | 业务状态;I初始化；S处理成功；F处理失败；E处理异常 |
| `memo` | varchar(255) | 备注;处理成功；已开卡；passport失败；异常code归类 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`data_id`
- `idx_data_key`:batch_code, data_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

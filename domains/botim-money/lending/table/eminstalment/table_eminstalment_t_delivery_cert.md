---
id: tbl_eminstalment_t_delivery_cert
object_type: Table
name: 保存在发货成功后rd传来的证明照片 (t_delivery_cert)
aliases: [t_delivery_cert, eminstalment.t_delivery_cert]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 保存在发货成功后rd传来的证明照片 (t_delivery_cert)

## 用途
物理表 `eminstalment.t_delivery_cert`,主键 `id`。保存在发货成功后rd传来的证明照片。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `goods_order_no` | varchar(64) | 商品订单号 |
| `type` | smallint(4) | 待补 |
| `oss_path` | varchar(64) | 文件在ufs中的保存路径 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_gt`:goods_order_no, type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

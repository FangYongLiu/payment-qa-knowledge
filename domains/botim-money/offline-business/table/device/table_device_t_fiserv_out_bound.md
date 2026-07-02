---
id: tbl_device_t_fiserv_out_bound
object_type: Table
name: fiserv out bound 文件信息 (t_fiserv_out_bound)
aliases: [t_fiserv_out_bound, device.t_fiserv_out_bound]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: device schema DDL
tags: [offline-business, device]
sensitivity: normal
related_services: []
---

# fiserv out bound 文件信息 (t_fiserv_out_bound)

## 用途
物理表 `device.t_fiserv_out_bound`,主键 `id`。fiserv out bound 文件信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `order_id` | varchar(50) | 订单号 |
| `out_bound_file_path` | varchar(200) | outBound文件路径 |
| `in_bound_file_path` | varchar(200) | outBound文件路径 |
| `out_bound_time` | timestamp | outbound时间 · 可空 |
| `source` | varchar(32) | 来源 |
| `merchant_name` | varchar(64) | 商户名称 · 可空 |
| `city` | varchar(64) | 城市 · 可空 |
| `tid` | varchar(50) | TID |
| `mid` | varchar(50) | MID |
| `store_id` | varchar(50) | 门店ID |
| `customer_reference` | varchar(50) | 客户参考号 · 可空 |
| `client` | varchar(30) | 客户端名称 · 可空 |
| `item_no` | varchar(30) | 商户编号 · 可空 |
| `software` | varchar(10) | 版本号 · 可空 |
| `serial_no` | varchar(32) | 序号 · 可空 |
| `store_status` | varchar(30) | 库存状态 · 可空 |
| `config_status` | varchar(32) | 配置状态 CREATED; CONFIGED |
| `mcc` | varchar(10) | MCC · 可空 |
| `created_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `uid_tid`:tid (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

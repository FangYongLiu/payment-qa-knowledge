---
id: tbl_acquireii_t_fiserv_sale_void_ops_order
object_type: Table
name: Fiserv Sale Void 订单表 (t_fiserv_sale_void_ops_order)
aliases: [t_fiserv_sale_void_ops_order, acquireii.t_fiserv_sale_void_ops_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# Fiserv Sale Void 订单表 (t_fiserv_sale_void_ops_order)

## 用途
物理表 `acquireii.t_fiserv_sale_void_ops_order`,主键 `global_id`。salevoid订单。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `request_no` | varchar(200) | 等同于requestIdentity.requestNo.查询方便 |
| `mis_order_no` | varchar(200) | 商户mis系统订单号 · 可空 |
| `origin_global_id` | bigint | 原始订单号 |
| `retransmission` | int | 重发计数 |
| `device_id` | varchar(200) | 发起方设备id |
| `partner_id` | varchar(32) | 发起方memberId |
| `res_payload_token` | varchar(32) | 返回ues_token · 可空 |
| `current_cmd_id` | bigint | 当前cmdid · 可空 |
| `channel_param_id` | bigint | 渠道参数id · 可空 |
| `status` | varchar(50) | 收单状态 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |
| `type` | varchar(50) | type · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_fsvoo_ct`:created_time
- `i_fsvoo_lut`:last_updated_time
- `i_fsvoo_ogi`:origin_global_id
- `i_fsvoo_rn`:request_no

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引,勿混用。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增、防覆盖。
- **幂等**:同一 `request_no` 不应重复落单。
- **关联原单**:`origin_global_id` 应能追溯到原始订单。
- **device 维度**:按 `device_id` 组织的批次/结算通常唯一,注意重复校验。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。

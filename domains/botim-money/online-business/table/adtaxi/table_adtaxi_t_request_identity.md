---
id: tbl_adtaxi_t_request_identity
object_type: Table
name: 请求标识表 (t_request_identity)
aliases: [t_request_identity, adtaxi.t_request_identity]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adtaxi schema DDL
tags: [online-business, 出租车支付, adtaxi]
sensitivity: normal
related_services: [svc_adtaxi]
---

# 请求标识表 (t_request_identity)

## 用途
物理表 `adtaxi.t_request_identity`,主键 `id`。请求标识。属出租车支付服务 [[svc_adtaxi]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_adtaxi]](= `related_services`)。
- **谁读写它**:出租车支付链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 退款全局号 |
| `issuer_type` | varchar(200) | 发起人类型 |
| `issuer_code` | varchar(200) | 发起人代码 |
| `request_no` | varchar(200) | 商户订单号 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `i_ri_no`:request_no

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。

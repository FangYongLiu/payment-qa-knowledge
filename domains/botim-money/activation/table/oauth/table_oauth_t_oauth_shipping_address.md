---
id: tbl_oauth_t_oauth_shipping_address
object_type: Table
name: 收货地址 (t_oauth_shipping_address)
aliases: [t_oauth_shipping_address, oauth.t_oauth_shipping_address]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: oauth schema DDL
tags: [activation, oauth]
sensitivity: normal
related_services: []
---

# 收货地址 (t_oauth_shipping_address)

## 用途
物理表 `oauth.t_oauth_shipping_address`,主键 `id`。收货地址。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `member_id` | varchar(64) | 会员标识 |
| `first_name` | varchar(16) | 收货人首名 |
| `last_name` | varchar(16) | 收货人尾名 |
| `phone_number` | varchar(16) | 手机号码 |
| `alternative_phone_number` | varchar(16) | 可选手机 |
| `email` | varchar(64) | 邮箱 |
| `continent_id` | bigint | 洲际标识。依赖t_oauth_division.id。一级地址 |
| `country_id` | bigint | 国家地区标识。依赖t_oauth_division.id。二级地址 |
| `province_id` | bigint | 省份标识。依赖t_oauth_division.id。三级地址 |
| `city_id` | bigint | 地级市标识。依赖t_oauth_division.id。四级地址 |
| `district_id` | bigint | 区县标识。依赖t_oauth_division.id。五级地址 |
| `township_id` | bigint | 镇乡标识。依赖t_oauth_division.id。六级地址 |
| `street_id` | bigint | 街道标识。依赖t_oauth_division.id。七级地址 |
| `continent_name` | varchar(99) | 洲际名字。一级地址。冗余 |
| `country_name` | varchar(99) | 国家地区名字。二级地址。冗余 |
| `province_name` | varchar(99) | 省份名字。三级地址。冗余 |
| `city_name` | varchar(99) | 地级市名字。四级地址。冗余 |
| `district_name` | varchar(99) | 区县名字。五级地址。冗余 |
| `township_name` | varchar(99) | 镇乡名字。六级地址。冗余 |
| `street_name` | varchar(99) | 街道。七级地址。冗余 |
| `address_line1` | varchar(255) | 详细地址 |
| `address_line2` | varchar(255) | 详细地址2 |
| `address_line3` | varchar(255) | 详细地址3 |
| `as_default` | varchar(2) | 是否默认 |
| `remark` | varchar(255) | 备注 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- `i_osa_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

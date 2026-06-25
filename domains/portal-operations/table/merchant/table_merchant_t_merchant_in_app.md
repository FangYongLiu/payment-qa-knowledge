---
id: tbl_merchant_t_merchant_in_app
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_merchant_in_app
subdomain: merchant
module: null
sensitivity: normal
name: 商户app(t_merchant_in_app)
aliases:
- t_merchant_in_app
related_services:
- svc_merchant
related_scenarios: []
---
# 商户app(t_merchant_in_app)

## 用途
商户app。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | order id |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `name` | varchar(50) | NOT NULL | app名称 |
| `mobile_site_url` | varchar(128) |  | 手机网站URL |
| `type` | varchar(20) | NOT NULL | 类型 MOBILE, WEB |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建 ENABLED 已可用 INVALID 不可用 |
| `icon_path` | varchar(256) | NOT NULL | icon路径 |
| `description` | varchar(256) |  | 描述 |
| `support_android_launch` | varchar(20) | NOT NULL | 是否支持安卓启动 |
| `support_ios_launch` | varchar(20) | NOT NULL | 是否支持苹果启动 |
| `signature` | varchar(256) |  | app签名 |
| `android_package_name` | varchar(256) |  | 安卓包名 |
| `android_download_link` | varchar(256) |  | 安卓下载链接 |
| `bundle_id` | varchar(256) |  | bundle id |
| `ios_download_link` | varchar(256) |  | 苹果下载链接 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `oauth_client_id` | varchar(255) |  | oauth 客户端id |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_merchant_t_pay_link
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_pay_link
subdomain: merchant
module: null
sensitivity: normal
name: paylink(t_pay_link)
aliases:
- t_pay_link
related_services:
- svc_merchant
related_scenarios: []
---
# paylink(t_pay_link)

## 用途
paylink。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `merchant_id` | bigint | NOT NULL | 商户id |
| `merchant_mid` | varchar(32) | NOT NULL | 商户mid |
| `product_title` | varchar(300) |  | 产品title |
| `amount_type` | varchar(32) | NOT NULL | 金额类型 FIX 固定金额，CUSTOM 用户输入 |
| `fix_amount` | decimal(19,4) |  | 固定金额 |
| `logo_path` | varchar(200) |  | logo图片路径 |
| `button_text` | varchar(200) |  | 按钮文本 |
| `button_icon` | varchar(128) |  | 按钮图标 |
| `button_width` | decimal(10,3) |  | 按钮宽度 |
| `button_color` | varchar(50) |  | 按钮颜色 |
| `text_color` | varchar(50) |  | 文本颜色 |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `show_name` | char |  | is show merchant name |
| `show_email` | char |  | is show email |
| `show_mobile` | char |  | is show mobile |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_merchant_t_pay_page
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
- t_pay_page
subdomain: merchant
module: null
sensitivity: normal
name: paypage(t_pay_page)
aliases:
- t_pay_page
related_services:
- svc_merchant
related_scenarios: []
---
# paypage(t_pay_page)

## 用途
paypage。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `merchant_mid` | varchar(32) | NOT NULL | 商户mid |
| `logo_path` | varchar(200) |  | logo图片路径 |
| `font` | varchar(50) |  | 字体 |
| `model` | varchar(10) | NOT NULL | 深色模式 |
| `secondary_color_light` | varchar(50) |  | 浅色二级色 |
| `primary_color_light` | varchar(50) |  | 浅色主色 |
| `primary_color_dark` | varchar(50) |  | 深色主色 |
| `secondary_color_dark` | varchar(50) |  | 深色二级色 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `show_lan_btn` | char |  | 是否显示语言切换按钮 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UIDX_MID` 唯一 (merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

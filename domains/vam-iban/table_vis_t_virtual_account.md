---
id: tbl_vis_t_virtual_account
object_type: Table
domain: vam-iban
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:071c6f83-3a57-411e-9cdb-e1ef3b1d92b8
tags: []
subdomain: null
module: null
sensitivity: normal
name: vis.t_virtual_account 虚拟账户表
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储用户 IBAN 虚拟账户信息。用户在 PayBy App 充值入口选择 Bank Account Transfer 并点击激活后,申请数据落地到本表,通过 `mid`/`member_id` 与用户关联。后续由 `vis_ibanAccountRetryJob` 批次处理(除 lean 场景外的 fab 用户申请),调用 fab 更新账户状态。

## 关键列
- `id`:主键(数值型),示例值 112。
- `member_id`:关联用户标识(对应 mid),示例值 100000056400。
- `hierarchy_name` / `hierarchy_type`:层级名称与类型(如 hierarchy_type=P)。
- `member_type`:成员类型(如 P)。
- `name`:用户名称(示例 P3090095)。
- `email` / `mobile_no`:联系邮箱与手机号(初始示例中 email 为 NULL,mobile_no=P2926593)。
- `account_type`:账户类型(示例 P&C)。
- `address_country` / `address_city` / `address_details`:地址相关字段。
- `file_id`:文件标识(数值型,初始为 NULL)。
- `status`:账户状态。
  - `Initial`:申请落库后的初始状态(激活后未完成 fab 处理;VIP 用户点击 Free Active 补充姓名后落库时也是 Initial)。
  - `Valid`:经 `vis_ibanAccountRetryJob` 批次触发并调用 fab 成功后更新为 Valid。
- `request_type`:请求类型(示例 A)。
- `communicate_status`:通信状态(示例 I)。
- `message`:消息字段(初始为 NULL)。
- `extension`:扩展字段(初始为 NULL)。
- `iban_no`:IBAN 号。当 IBAN 有库存时落库填充;无库存时前端申请落库 `iban_no=NULL`,需人工补充后等待 job 重试。
- `gmt_create` / `gmt_modified` / `gmt_complete`:创建/修改/完成时间戳(初始记录中 `gmt_complete` 为 NULL)。
- `notify_status`:通知状态(初始为 NULL)。
- `maker_remarks`:制单备注(初始为 NULL)。
- `enrichment_field`:补充字段(初始为 NULL)。
- `primary_id` / `alias` / `parent_mapping`:主标识、别名、父级映射(初始均为 NULL)。

## 主键/索引
- 主键:`id`(数值型)。
- 其他索引:原文未提供。

## 校验点(QA 关注)
- 普通用户在 App 点击激活后,校验本表是否生成记录、`member_id`/mid 是否正确关联、`status=Initial`、`iban_no=NULL`(无库存场景)。
- 新建初始记录的典型字段值参考:`status=Initial`、`iban_no=NULL`、`gmt_complete=NULL`、`notify_status=NULL`、`message=NULL`、`extension=NULL`、`maker_remarks=NULL`、`enrichment_field=NULL`、`primary_id=NULL`、`alias=NULL`、`parent_mapping=NULL`、`request_type=A`、`communicate_status=I`。
- VIP 用户点击 Free Active 补充姓名信息时无校验,仍需确认数据落库且 `status=Initial`。
- 非 lean 场景的 fab 用户申请,需确认落库后由 `vis_ibanAccountRetryJob` 批次处理,job 触发后状态由 Initial 更新为 Valid。
- IBAN 库存为空场景:确认前端申请落库时 `iban_no=NULL`,可人工补充 IBAN 数据后由 job 重试,最终状态变为 Valid。
- 配合 mock 配置 `vis.notification.mock=Y` 时不会调用 fab,需关注本表状态流转是否符合 mock 预期。
- 可使用 `select * from vis.t_virtual_account order by gmt_create desc` 按创建时间倒序排查最新落库记录。

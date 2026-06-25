---
id: ts_payment_db_navigation
object_type: Troubleshooting
name: 支付链路数据库库表速查与排查导航
aliases:
- 常用数据库指南
- 库表速查
- payment db navigation
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289264; wiki:79d1eee0-a479-47fd-8b3d-ec12172156f3
tags:
- database
- troubleshooting
- 库表速查
- 排查导航
related_services:
- svc_tradeii
- svc_deposit
- svc_reconciliation
related_tables: []
related_logs: []
related_failures: []
---

# 支付链路数据库库表速查与排查导航

## 症状
排查一笔交易 / 一个会员 / 一个商户的问题时,不知道该查哪个库、哪张表、用什么唯一标识贯穿,导致定位数据缓慢。本页给出按业务域的库表速查表与标准排查链路,作为定位数据的导航入口。

> 各张表的字段与详细说明,优先查对应域已建的 Table 对象(见下方「相关 Table 对象」),本页只做导航,不重复字段明细。

## 关联关系
- **涉及服务**:[[svc_tradeii]](中台交易)、[[svc_deposit]](充值)、[[svc_reconciliation]](对账/结算)(= `related_services`)。
- 其余服务(member / acquireii / mhtfundout / transfer / acs 网关等)落在其它业务域,见各域服务对象,本页不重复连边。

## 可能根因
本页是导航/速查,不针对单一根因;用于在数据定位阶段快速找到目标库表与贯穿标识。

## 排查步骤

### 标准排查链路(一笔交易)
按链路逐层定位:
1. **接入鉴权 `acs`** —— 验签 / 接口权限 / IP 白名单(`t_key_config`、`t_gateway_merchant_api_auth`、`t_gateway_api_group`、`t_gateway_api_group_relation`、`t_reffer_list`)。
2. **订单与支付 `tradeii` / `acquireii`** —— 交易主单与支付订单。
3. **账户变动 `dpm`** —— 外部 / 内部账户余额明细。
4. **对账 `statementii`** —— 账期、对账单登记 / 模板 / 任务 / 文件、收单对账统计。

### 维度定位约定
- **会员维度**:优先用 `member.tm_member_identity` 的 `IDENTITY` 唯一标识贯穿其它会员相关表。
- **商户维度**:先确认 `merchant.t_merchant` 的 `mid`(商户号)与 `id`(商户 ID),再关联门店(`t_store`,`merchant_id` 关联)、员工(`t_staff` / `t_staff_role`)、设备。
- **认证维度**:`member.tr_verify_ref` 类型枚举 `1` 身份证 / `11` 手机 / `12` 信箱;实体即对应的身份证号 / 手机号 / 邮箱,关联 `tr_verify_entity`(主键 `VERIFY_ENTITY_ID`)。
- **支付密码**:挂在操作员(`member.tm_operator`)下,密码在 `member.tr_password`。

### 按业务域的库表速查

**会员与账户(member / dpm)**
- `member.tm_member` 会员信息;`tm_member_identity` 会员唯一标识 `IDENTITY`;`tm_realname_entity` 实名信息。
- `tr_verify_entity` 认证实体;`tr_verify_ref` 认证关系;`tr_verify_entity_rel`。
- `tm_operator` 操作员;`tr_password` 支付密码;`td_config` 配置。
- `tr_member_device` 用户设备绑定;`tm_device` 设备信息(型号/系统)。
- `tr_member_account` 会员账户;`tr_bank_account` 个人银行卡。
- `dpm.t_dpm_outer_account` 会员外部账户;`t_dpm_outer_account_subset` 外部账户分户;`t_dpm_outer_account_sub_detail` 外部账户余额变动明细;`t_dpm_inner_account_detail` 内部账户余额明细。

**网关接入(acs)**
- `t_key_config` 公私钥;`t_gateway_merchant_api_auth` 接口权限;`t_gateway_api_group` 接口配置;`t_gateway_api_group_relation` 接口分组关系;`t_reffer_list` IP 白名单。
- 排查接口未授权:先看 `t_gateway_merchant_api_auth`,再结合 `t_gateway_api_group` / `t_gateway_api_group_relation` 确认接口归属分组;验签问题查 `t_key_config`;来源 IP 拦截查 `t_reffer_list`。

**商户与设备(merchant / device)**
- `merchant.t_merchant` 商户(`mid`/`id`);`t_store` 门店;`t_staff` / `t_staff_role` 员工与角色;`t_period` 账期;`t_auto_withdraw_registration` / `t_auto_withdraw_order` 定时出款设置与订单。
- `device.t_hardware_info` 设备信息;`t_merchant_device` 商户绑定设备;`t_active_code` 激活码;`t_device_apply_order` 设备申请;`t_device_key` 设备密钥。

**收单交易(acquireii)**
- `t_acquire_order` 收单交易;`t_payment_info` 收单支付信息;`t_refund_order` 收单退款。

**出款 / 转账(mhtfundout / transfer)**
- `mhtfundout.t_fundout_order` 出款订单;`t_payment_info` 出款支付信息;`t_fundout_account_beneficiary` 出款收款方。
- `transfer.t_transfer_order` 个人转账。

**中台交易(deposit / tradeii / fundout)**
- `deposit.t_deposit_order` 充值订单。
- `tradeii.t_trade_order` 交易主单;`t_order_ext` 交易订单扩展;`t_payment_order` 交易支付订单。
- `fundout.tt_fundout_order` 提现订单。

**账单 / 对账(statementii)**
- `t_statement_period` 账期;`t_statement_registration` 对账单登记;`t_statement_template` 对账单模板;`t_statement_task` 对账单任务;`t_statement_file` 对账单文件;`t_statement_pruchase_statistics` 收单对账统计。

**费率与定价(ppcenter / pbsdb)**
- `ppcenter`:`t_product_template` 产品模板 → `t_calculation_define` 费率定义 → `t_price_cal` 费率配置 → `t_product_apply_order` 产品申请 / `t_product_apply_info` 审核资料 → `t_package_define` 产品包 / `t_package_template_relation` 产品包与模板关联。
- `pbsdb`:`tb_pbs_price_strategy_unit` 费率策略;`tb_pbs_price_strategy_param` 策略详情;`tb_pbs_price_cal` 价格计算策略。

**生活中心**
- `marketorder.t_order` 订单;`marketgoods.t_goods_sku` 商品 SKU;`supplier.t_supplier_channel` 供应商渠道。

### 环境与连接(MySQL 实例)
不同测试环境的 MySQL 实例连接地址(账号密码见安全凭据管理,本页不落明文):

| 环境 | 实例别名 | mysql_uri |
| --- | --- | --- |
| sim | dbfunc2 | `dbfunc2.test2pay.com:3306` |
| dev | devdb1 | `dbdev1.test2pay.com:3306` |
| uat | rds1.uat-azure | `mysql-rds-uat-pby-aen-001.mysql.database.azure.com:3306` |
| stress | stressDB | 待补 |

账号约定:
- 用户名统一 `<模块>user`(少量例外:`reader`、`syncuser`、`prometheus`、`creditmareader`、`heartbeatreader`、`poweruser` 等)。
- 密码格式 `<模块>_<随机串>`,sim/dev/uat 三套互不相同;**stress 环境用户名与密码相等**。
- 具体账号密码属敏感凭据,按实际环境配置获取(待补:统一凭据来源)。

## 处理 / 规避
- 详细字段与样例查询见对应域已建的 Table 对象(见下);本页缺失字段处统一标「待补」,人工补充更新。
- 相关 Table 对象(跨域,字段明细在各自对象):
  - 会员:[[table_member_db]]、[[table_member_tr_bank_card_token]]、[[table_member_tr_deduct_channel]](wallet 域)
  - 收单:[[table_acquireii_t_acquire_order]]、[[table_acquireii_t_payment_info]]、[[table_acquireii_t_refund_order]]、[[table_mhtfundout_t_fundout_order]](online-business 域)
  - 商户 / 设备:[[table_merchant_db]]、[[table_merchant_device]](portal-operations 域)、[[table_device_db]]、[[table_active_code]]、[[table_device_apply_order]](offline-business 域)
  - 网关:[[table_acs_db]](risk 域)
  - 结算 / 对账:[[tbl_reconciliation_t_settlement_template]]、[[tbl_reconciliation_t_settlement_detail]](payment-core)
- dpm 账户明细表、tradeii / deposit / statementii / ppcenter / pbsdb 各表尚无独立 Table 对象:待补。

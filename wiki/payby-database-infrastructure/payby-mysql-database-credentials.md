---
title: PayBy MySQL 数据库连接与账号清单
domain: payment-database-reference
kind: wiki_page
slug: payby-mysql-database-credentials
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:3a2ee293-8efa-43db-ac99-36d5fedd176d
tags: []
---

# PayBy MySQL 数据库连接与账号清单

汇总 PayBy 各测试环境（sim / dev / uat / stress）的 MySQL 实例连接地址，以及各业务模块对应的数据库账号与密码（用户名形如 `xxxuser`，密码形如 `xxx_<随机串>`）。

## 实例连接地址

| Instance | mysql_uri |
| --- | --- |
| sim | `dbfunc2.test2pay.com:3306` |
| dev | `dbdev1.test2pay.com:3306` |
| uat | `mysql-rds-uat-pby-aen-001.mysql.database.azure.com:3306` |
| stress | （待补充） |

实例别名对照：

- sim → `dbfunc2`（`dbfunc2.test2pay.com`）
- dev → `devdb1`（`dbdev1.test2pay.com`）
- uat → `rds1.uat-azure.test2pay.com`
- stress → `stressDB`（用户名与密码相等）

## 账号约定

- 用户名统一格式为 `<模块>user`（少量例外：`reader`、`syncuser`、`prometheus`、`creditmareader`、`heartbeatreader`、`poweruser` 等）。
- 密码格式为 `<模块>_<随机字符串>`，sim/dev/uat 三套环境互不相同。
- stress 环境特殊约定：**用户名和密码相等**。
- uat 环境密码原文留空（请按实际环境配置确认）。

## 通用只读 / 同步账号

| 账号 | sim 密码 | dev 密码 | uat 密码 |
| --- | --- | --- | --- |
| reader | `reader_j0kqgaHxsI5O6j` | `reader_j0kqgaHxsI5O6j` | `reader_kpwRMI1nifffNV` |
| syncuser | — | — | （uat 独有，密码留空） |
| prometheus | `prometheus_aGlmLok7F6E2bv` | `prometheus_aGlmLok7F6E2bv` | （uat 留空） |
| heartbeatuser | `heartbeat_zTsHX9okvuUQt9` | `heartbeat_zTsHX9okvuUQt9` | （uat 留空） |
| heartbeatreader | `heartbeat_lxWCI9F56o7hNI` | `heartbeat_lxWCI9F56o7hNI` | （uat 留空） |
| creditmareader | `creditma_ztt6BmoWK8x0Ur` | `creditma_LvSwtbQY3HU27o` | （uat 留空） |
| poweruser | — | — | （uat 独有） |

## 业务模块账号（sim / dev）

下表按模块列出 sim、dev 两套环境的密码；uat 用户名与之相同，密码以 uat 实际配置为准（原文留空）。

### 支付 / 交易

| user | sim 密码 | dev 密码 |
| --- | --- | --- |
| paymentuser | `payment_PU4qADVP1myYv6` | `payment_RewxvtJu67fgVB` |
| cspaymentuser | `cspayment_mlzFmG7W1YbZ6Q` | `cspayment_ejL12c0gu8mYtr` |
| tradeuser | `trade_dHLnexB2tcmfFS` | `trade_uGPWbJ3g728vqE` |
| tradeiiuser | `tradeii_IalPrSn2PlWL07` | `tradeii_vPsiWUOavgkwQc` |
| gptradeuser | `gptrade_EJ7k2ZkN3NWYsl` | `gptrade_leTa4deY0JYwWc` |
| cctradeuser | `cctrade_KXdEgoUe4NxuNK` | `cctrade_DLxWd9kC7CmNvc` |
| acquireuser | `acquire_BXrGVsgdfqA6Rt` | `acquire_CHhmAjoEQqR7T2` |
| acquireiiuser | `acquireii_QzK81JxSlz488D` | `acquireii_uOagyEOWb8rbDk` |
| ccacquireuser | `ccacquire_xZspUcs8QMoHe2` | `ccacquire_r2n8iz1x2R4MIx` |
| cashdeskuser | `cashdesk_UZXQgEpnL0mojh` | `cashdesk_C3QCRucvPobSwU` |
| casheatmuser | `casheatm_ZhZcew5epT1TdW` | `casheatm_QSVPkRk87DTixl` |
| counteruser | `counter_vYSNcoyVKXs29V` | `counter_VkWw4mYcdZMAQK` |
| facepayuser | `facepay_zvVWEIkZ2df1KZ` | `facepay_TnosYIZ8EriSzG` |
| socialpayuser | `socialpay_WFizWhKiR0jGZZ` | `socialpay_AXSPBk2IO7oTdn` |
| subscribepayuser | `subscribepay_SuOyW3IWwHdDic` | `subscribepay_OXZDNnFu8NDKoQ` |
| paylateruser | `paylater_GbbTStEC9jaxeR` | `paylater_TnHp6E35LPblnJ` |
| preauthuser | `preauth_e1z0VWCj1cbOQo` | `preauth_FroUrd6AhneQTt` |
| transferuser | `transfer_EnXdGMCf0CMvJX` | `transfer_MaeW3tkIFUHZhP` |
| cctransferuser | `cctransfer_nN7NyNFLhYehIv` | `cctransfer_UgwQySnlBTZLPh` |
| remittanceuser | `remittance_Jx5JZjsqbIrM43` | `remittance_yQ5OvmVMiy5I7G` |

### 资金 / 账户 / 资产

| user | sim 密码 | dev 密码 |
| --- | --- | --- |
| deposituser | `deposit_Gic8ZS2Au7VsWt` | `deposit_eZSf3z7cY1yPGR` |
| ccdeposituser | `ccdeposit_slTn3VAvkCY8AE` | `ccdeposit_WSPa9hEAaq2pvR` |
| fundoutuser | `fundout_QUbgXRcuxa9IDB` | `fundout_jiSq8N6tfA5EWh` |
| mhtfundoutuser | `mhtfundout_WUxir6SoG484Up` | `mhtfundout_OWPxIr4PHGTwo3` |
| ccwithdrawuser | `ccwithdraw_jZxvHqviNk3Dsb` | `ccwithdraw_WGDCygC5NIY63z` |
| escrowuser | `escrow_Le9BTQpX0UJHUI` | `escrow_u4iV3uwaNmaora` |
| dpmuser | `dpm_dQLMq1dAP6bxt0` | `dpm_zZBxNPfzYHK7vo` |
| ccdpmuser | `ccdpm_5WAoCiFIIeh6cQ` | `ccdpm_eoUO73k9ChK9Qd` |
| limituser | `limit_kf5208SCQxOlzb` | `limit_l6FpUISHD0oky1

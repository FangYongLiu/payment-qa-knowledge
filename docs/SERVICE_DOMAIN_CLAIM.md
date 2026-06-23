# 服务认领表（可选 · 按需自取）

> 由 `scripts/import_services.py` 从 SYSTEM_APP_INVENTORY.md 生成。共 282 个服务 / 242 个 app_group。
> **认领是可选的**：全部 282 个服务骨架已激活在中性域 `service-catalog`，Bimo 已能
> 检索到「有哪些服务、属于哪个 app 组」。**只有要为某服务建测试知识时才认领**——填下面的
> `domain`(12 业务域之一) / `owner`，我据此把文件移到 `domains/<domain>/`、写 frontmatter、补内容。
> 不认领的服务一直保持骨架即可（基础设施/mock/admin 等长尾通常无需认领）。
> **同一 app_group 通常属于同一个域**——可整组一起认领。

12 个业务域：online-business / offline-business / payment-core / payment-tools / portal-operations / remittance / wallet / card / kyc / risk / wps / compliance

## app_group `bd002`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mysql-member-sync | `svc_mysql_member_sync` |  |  |

## app_group `bd004`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| data-server | `svc_data_server` |  |  |
| uae-data-server | `svc_uae_data_server` |  |  |

## app_group `bd006`（3 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| auth_server | `svc_auth_server` |  |  |
| crawl-leantech-server | `svc_crawl_leantech_server` |  |  |
| crawl-server | `svc_crawl_server` |  |  |

## app_group `bd007`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| feature-calculate-server | `svc_feature_calculate_server` |  |  |
| feature-calculate-server-new | `svc_feature_calculate_server_new` |  |  |

## app_group `gp001`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ues-ws | `svc_ues_ws` |  |  |

## app_group `gp002`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cmf | `svc_cmf` |  |  |
| cmf-task | `svc_cmf_task` |  |  |

## app_group `gp003`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pbs | `svc_pbs` |  |  |

## app_group `gp004`（3 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| dpm-accounting | `svc_dpm_accounting` |  |  |
| dpm-manager | `svc_dpm_manager` |  |  |
| dpm-task | `svc_dpm_task` |  |  |

## app_group `gp005`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| member | `svc_member` |  |  |

## app_group `gp006`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| payment | `svc_payment` |  |  |

## app_group `gp007`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cashdesk-api | `svc_cashdesk_api` |  |  |

## app_group `gp008`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| acs | `svc_acs` |  |  |

## app_group `gp009`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| voucher | `svc_voucher` |  |  |

## app_group `gp011`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| deposit | `svc_deposit` |  |  |

## app_group `gp012`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| fundout | `svc_fundout` |  |  |

## app_group `gp013`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pns | `svc_pns` |  |  |

## app_group `gp014`（3 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pfs-basis | `svc_pfs_basis` |  |  |
| pfs-manager | `svc_pfs_manager` |  |  |
| pfs-payment | `svc_pfs_payment` |  |  |

## app_group `gp016`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| outman | `svc_outman` |  |  |

## app_group `gp018`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| spring-boot-admin | `svc_spring_boot_admin` |  |  |

## app_group `gp019`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| spring-cloud-config | `svc_spring_cloud_config` |  |  |

## app_group `gp020`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| dubbo-admin | `svc_dubbo_admin` |  |  |

## app_group `gp021`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| elasticjob-console | `svc_elasticjob_console` |  |  |

## app_group `gp022`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| software-management | `svc_software_management` |  |  |

## app_group `gp023`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| basis | `svc_basis` |  |  |

## app_group `gp024`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cgs | `svc_cgs` |  |  |

## app_group `gp026`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pos-gateway | `svc_pos_gateway` |  |  |

## app_group `gp028`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| sgs | `svc_sgs` |  |  |

## app_group `gp030`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| query | `svc_query` |  |  |
| query-datasync | `svc_query_datasync` |  |  |

## app_group `gp031`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| counter | `svc_counter` |  |  |

## app_group `gp032`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| personal | `svc_personal` |  |  |

## app_group `gp033`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| xbh-gateway | `svc_xbh_gateway` |  |  |

## app_group `gp034`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| authpay | `svc_authpay` |  |  |

## app_group `gp035`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| socialpay | `svc_socialpay` |  |  |

## app_group `gp037`（3 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mns-listener | `svc_mns_listener` |  |  |
| mns-main | `svc_mns_main` |  |  |
| mns-scheduler | `svc_mns_scheduler` |  |  |

## app_group `gp038`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| bigdata-admin | `svc_bigdata_admin` |  |  |
| bigdata-ws | `svc_bigdata_ws` |  |  |

## app_group `gp039`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| fcw | `svc_fcw` |  |  |

## app_group `gp040`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pts | `svc_pts` |  |  |

## app_group `gp041`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pbs-bos | `svc_pbs_bos` |  |  |

## app_group `gp042`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pcs | `svc_pcs` |  |  |

## app_group `gp043`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| reconciliation | `svc_reconciliation` |  |  |

## app_group `gp044`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| merchant | `svc_merchant` |  |  |

## app_group `gp045`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| merchant-console-frontend | `svc_merchant_console_frontend` |  |  |

## app_group `gp046`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pcm | `svc_pcm` |  |  |

## app_group `gp047`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ppcenter | `svc_ppcenter` |  |  |

## app_group `gp048`（10 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| hive-activities | `svc_hive_activities` |  |  |
| hive-bank-console | `svc_hive_bank_console` |  |  |
| hive-cashier | `svc_hive_cashier` |  |  |
| hive-checkout | `svc_hive_checkout` |  |  |
| hive-developers | `svc_hive_developers` |  |  |
| hive-m-topay | `svc_hive_m_topay` |  |  |
| hive-mcashier | `svc_hive_mcashier` |  |  |
| hive-merchant-console | `svc_hive_merchant_console` |  |  |
| hive-portal | `svc_hive_portal` |  |  |
| hive-utilities | `svc_hive_utilities` |  |  |

## app_group `gp050`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cps | `svc_cps` |  |  |

## app_group `gp053`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| transfer | `svc_transfer` |  |  |

## app_group `gp054`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| device | `svc_device` |  |  |

## app_group `gp055`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| sqlmonitor | `svc_sqlmonitor` |  |  |

## app_group `gp056`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| csc | `svc_csc` |  |  |

## app_group `gp057`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| fido-mgmt | `svc_fido_mgmt` |  |  |
| fidoservice | `svc_fidoservice` |  |  |

## app_group `gp058`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cash-eatm | `svc_cash_eatm` |  |  |

## app_group `gp060`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| authorization-service | `svc_authorization_service` |  |  |

## app_group `gp062`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| h2h | `svc_h2h` |  |  |

## app_group `gp064`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| customer-frontend | `svc_customer_frontend` |  |  |

## app_group `gp065`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| porter | `svc_porter` |  |  |

## app_group `gp066`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| channel-mobile-ding | `svc_channel_mobile_ding` |  |  |

## app_group `gp068`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| marketing | `svc_marketing` |  |  |

## app_group `gp069`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| acquireii | `svc_acquireii` |  |  |

## app_group `gp070`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| csimple | `svc_csimple` |  |  |

## app_group `gp071`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| merchant-frontend | `svc_merchant_frontend` |  |  |

## app_group `gp073`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| supplier | `svc_supplier` |  |  |

## app_group `gp074`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| life-center | `svc_life_center` |  |  |

## app_group `gp075`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| market-goods | `svc_market_goods` |  |  |

## app_group `gp076`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| market-order | `svc_market_order` |  |  |

## app_group `gp077`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| user-profile-scheduler | `svc_user_profile_scheduler` |  |  |

## app_group `gp078`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| kyc | `svc_kyc` |  |  |

## app_group `gp079`（4 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| grc-check-identity-provider | `svc_grc_check_identity_provider` |  |  |
| grc-component-connect-provider | `svc_grc_component_connect_provider` |  |  |
| grc-cps-provider | `svc_grc_cps_provider` |  |  |
| grc-engine-provider | `svc_grc_engine_provider` |  |  |

## app_group `gp080`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cqm | `svc_cqm` |  |  |

## app_group `gp081`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cbm | `svc_cbm` |  |  |

## app_group `gp083`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| merchant-fundout | `svc_merchant_fundout` |  |  |

## app_group `gp084`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| otpmock | `svc_otpmock` |  |  |
| otps | `svc_otps` |  |  |

## app_group `gp085`（7 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| oauth-client-service-cgs-impl | `svc_oauth_client_service_cgs_impl` |  |  |
| resource-service-cgs-impl | `svc_resource_service_cgs_impl` |  |  |
| resource-service-rpc-dubbo-provider | `svc_resource_service_rpc_dubbo_provider` |  |  |
| resource-service-sgs-impl | `svc_resource_service_sgs_impl` |  |  |
| resource-service-web | `svc_resource_service_web` |  |  |
| session-service-cgs-impl | `svc_session_service_cgs_impl` |  |  |
| session-service-rpc-dubbo-provider | `svc_session_service_rpc_dubbo_provider` |  |  |

## app_group `gp086`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cbs | `svc_cbs` |  |  |

## app_group `gp087`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-mcii | `svc_qpay_mcii` |  |  |

## app_group `gp088`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-fs | `svc_qpay_fs` |  |  |

## app_group `gp089`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| agreements-static | `svc_agreements_static` |  |  |

## app_group `gp091`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cms | `svc_cms` |  |  |

## app_group `gp092`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-pl-channel | `svc_qpay_pl_channel` |  |  |

## app_group `gp093`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cards | `svc_cards` |  |  |

## app_group `gp094`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| basis-cms | `svc_basis_cms` |  |  |

## app_group `gp095`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| paylater | `svc_paylater` |  |  |

## app_group `gp096`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| css | `svc_css` |  |  |

## app_group `gp098`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| green-points | `svc_green_points` |  |  |

## app_group `gp099`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| gpoint | `svc_gpoint` |  |  |

## app_group `gp100`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ons | `svc_ons` |  |  |

## app_group `gp101`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| authorization-token | `svc_authorization_token` |  |  |

## app_group `gp103`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| kiosk-channel | `svc_kiosk_channel` |  |  |

## app_group `gp104`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| escrow | `svc_escrow` |  |  |

## app_group `gp105`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| marketing-event | `svc_marketing_event` |  |  |

## app_group `gp106`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| iso8583-gateway | `svc_iso8583_gateway` |  |  |

## app_group `gp107`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| contract | `svc_contract` |  |  |

## app_group `gp110`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| gptrade | `svc_gptrade` |  |  |

## app_group `gp114`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ufs2 | `svc_ufs2` |  |  |

## app_group `gp116`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| shortlink | `svc_shortlink` |  |  |

## app_group `gp120`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| protocol | `svc_protocol` |  |  |
| protocol-duplicate | `svc_protocol_duplicate` |  |  |

## app_group `gp122`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| invoice | `svc_invoice` |  |  |

## app_group `gp123`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| tradeii | `svc_tradeii` |  |  |

## app_group `gp124`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| router | `svc_router` |  |  |

## app_group `gp125`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| adtaxi | `svc_adtaxi` |  |  |

## app_group `gp126`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cmsii | `svc_cmsii` |  |  |

## app_group `gp127`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mcs | `svc_mcs` |  |  |

## app_group `gp129`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| channel-paykii | `svc_channel_paykii` |  |  |

## app_group `gp130`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| credit-business | `svc_credit_business` |  |  |

## app_group `gp131`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| marketnotify | `svc_marketnotify` |  |  |

## app_group `gp133`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| vcs | `svc_vcs` |  |  |

## app_group `gp134`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| statementii | `svc_statementii` |  |  |

## app_group `gp135`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| member-front | `svc_member_front` |  |  |

## app_group `gp136`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| custom | `svc_custom` |  |  |

## app_group `gp137`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| asset-info | `svc_asset_info` |  |  |

## app_group `gp138`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| crypto-currency-exchange | `svc_crypto_currency_exchange` |  |  |

## app_group `gp139`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| facepay-api | `svc_facepay_api` |  |  |

## app_group `gp140`（3 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ccdpm-accounting | `svc_ccdpm_accounting` |  |  |
| ccdpm-manager | `svc_ccdpm_manager` |  |  |
| ccdpm-task | `svc_ccdpm_task` |  |  |

## app_group `gp141`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mssii | `svc_mssii` |  |  |

## app_group `gp142`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| quotation | `svc_quotation` |  |  |

## app_group `gp144`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| holding | `svc_holding` |  |  |

## app_group `gp145`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-sales | `svc_cc_sales` |  |  |

## app_group `gp146`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-withdraw | `svc_cc_withdraw` |  |  |

## app_group `gp148`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| member-feature | `svc_member_feature` |  |  |

## app_group `gp149`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| vis | `svc_vis` |  |  |

## app_group `gp150`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| host | `svc_host` |  |  |

## app_group `gp151`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| host-gateway | `svc_host_gateway` |  |  |

## app_group `gp153`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| upic | `svc_upic` |  |  |

## app_group `gp154`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-channel-eth | `svc_cc_channel_eth` |  |  |

## app_group `gp155`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-deposit | `svc_cc_deposit` |  |  |

## app_group `gp156`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| exchange | `svc_exchange` |  |  |

## app_group `gp158`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-installment | `svc_qpay_installment` |  |  |

## app_group `gp159`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-channel-btc | `svc_cc_channel_btc` |  |  |

## app_group `gp160`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| comp-service | `svc_comp_service` |  |  |

## app_group `gp161`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| basis-merchant | `svc_basis_merchant` |  |  |

## app_group `gp162`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-transfer | `svc_cc_transfer` |  |  |

## app_group `gp163`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| coupon | `svc_coupon` |  |  |

## app_group `gp164`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| coupon-service | `svc_coupon_service` |  |  |

## app_group `gp165`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| coupon-gateway | `svc_coupon_gateway` |  |  |

## app_group `gp170`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-trade | `svc_cc_trade` |  |  |

## app_group `gp176`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-cashier | `svc_cc_cashier` |  |  |

## app_group `gp178`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| calculator | `svc_calculator` |  |  |

## app_group `gp180`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-acquire | `svc_cc_acquire` |  |  |

## app_group `gp181`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cc-channel-tron | `svc_cc_channel_tron` |  |  |

## app_group `gp184`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| df-calculation | `svc_df_calculation` |  |  |

## app_group `gp185`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| gadget | `svc_gadget` |  |  |

## app_group `gp186`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| 3ds2 | `svc_3ds2` |  |  |

## app_group `gp187`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-ni-channel | `svc_qpay_ni_channel` |  |  |

## app_group `gp188`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance | `svc_remittance` |  |  |

## app_group `gp189`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| marketing-campaign | `svc_marketing_campaign` |  |  |

## app_group `gp190`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| marketing-gateway | `svc_marketing_gateway` |  |  |

## app_group `gp192`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| fraud | `svc_fraud` |  |  |

## app_group `gp193`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cashierii | `svc_cashierii` |  |  |

## app_group `gp194`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| basis-customer | `svc_basis_customer` |  |  |

## app_group `gp195`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| tpay-nyu | `svc_tpay_nyu` |  |  |

## app_group `gp197`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| preauth | `svc_preauth` |  |  |

## app_group `gp199`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cloud-mis | `svc_cloud_mis` |  |  |

## app_group `gp200`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-fsii | `svc_qpay_fsii` |  |  |

## app_group `gp201`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-klip | `svc_qpay_klip` |  |  |

## app_group `gp202`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| kyc-service | `svc_kyc_service` |  |  |

## app_group `gp204`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| data-etl | `svc_data_etl` |  |  |

## app_group `gp205`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| deduct | `svc_deduct` |  |  |

## app_group `gp207`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| das | `svc_das` |  |  |

## app_group `gp209`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| aml | `svc_aml` |  |  |

## app_group `gp210`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| npss-gateway | `svc_npss_gateway` |  |  |

## app_group `gp212`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ppc | `svc_ppc` |  |  |

## app_group `gp213`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pos-exception-processor | `svc_pos_exception_processor` |  |  |

## app_group `gp216`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| rdgs | `svc_rdgs` |  |  |

## app_group `gp220`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| youstore-installment | `svc_youstore_installment` |  |  |

## app_group `gp221`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-cko | `svc_qpay_cko` |  |  |

## app_group `gp222`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| npss | `svc_npss` |  |  |

## app_group `gp223`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mock-datawire | `svc_mock_datawire` |  |  |

## app_group `gp225`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| asite | `svc_asite` |  |  |

## app_group `gp227`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| push-to-pay | `svc_push_to_pay` |  |  |

## app_group `gp230`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pus | `svc_pus` |  |  |

## app_group `gp231`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| escrowii | `svc_escrowii` |  |  |

## app_group `gp232`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-aplus | `svc_qpay_aplus` |  |  |

## app_group `gp233`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| leanlink | `svc_leanlink` |  |  |

## app_group `gp234`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-lean | `svc_qpay_lean` |  |  |

## app_group `gp236`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| wechat-channel | `svc_wechat_channel` |  |  |

## app_group `gp237`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| payroll-core-service | `svc_payroll_core_service` |  |  |

## app_group `gp238`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ifb-channel | `svc_ifb_channel` |  |  |

## app_group `gp239`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| feebill | `svc_feebill` |  |  |

## app_group `gp240`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| household | `svc_household` |  |  |

## app_group `gp242`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| corporate-portal | `svc_corporate_portal` |  |  |

## app_group `gp243`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mock-channel | `svc_mock_channel` |  |  |

## app_group `gp244`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-nipos | `svc_qpay_nipos` |  |  |

## app_group `gp245`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-fts | `svc_qpay_fts` |  |  |

## app_group `gp247`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| datasavvy | `svc_datasavvy` |  |  |

## app_group `gp251`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| unified-merchant-portal | `svc_unified_merchant_portal` |  |  |

## app_group `gp252`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-nisocket | `svc_qpay_nisocket` |  |  |

## app_group `gp254`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| onboarding | `svc_onboarding` |  |  |

## app_group `gp257`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-swiftx | `svc_remittance_swiftx` |  |  |

## app_group `gp258`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| crs | `svc_crs` |  |  |

## app_group `gp259`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cregister | `svc_cregister` |  |  |

## app_group `gp261`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pix | `svc_pix` |  |  |

## app_group `gp262`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-niboarding | `svc_qpay_niboarding` |  |  |

## app_group `gp264`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-bdo | `svc_remittance_bdo` |  |  |

## app_group `gp267`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-mpgs | `svc_qpay_mpgs` |  |  |

## app_group `gp268`（2 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| bigdata-router | `svc_bigdata_router` |  |  |
| bigdata-router-admin | `svc_bigdata_router_admin` |  |  |

## app_group `gp269`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-enbd | `svc_qpay_enbd` |  |  |

## app_group `gp270`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| member-task | `svc_member_task` |  |  |

## app_group `gp274`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| bafl-channel | `svc_bafl_channel` |  |  |

## app_group `gp275`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| acquire2-query | `svc_acquire2_query` |  |  |

## app_group `gp276`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-ime | `svc_remittance_ime` |  |  |

## app_group `gp278`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| customer-service | `svc_customer_service` |  |  |

## app_group `gp279`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| commission | `svc_commission` |  |  |

## app_group `gp280`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| ni-mock | `svc_ni_mock` |  |  |

## app_group `gp281`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| officer | `svc_officer` |  |  |

## app_group `gp283`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pcbs | `svc_pcbs` |  |  |

## app_group `gp284`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pws | `svc_pws` |  |  |

## app_group `gp286`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| adg | `svc_adg` |  |  |

## app_group `gp287`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-ext | `svc_remittance_ext` |  |  |

## app_group `gp288`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| merchant-settlement | `svc_merchant_settlement` |  |  |

## app_group `gp289`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cns | `svc_cns` |  |  |

## app_group `gp290`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-fuze | `svc_remittance_fuze` |  |  |

## app_group `gp291`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| rtp | `svc_rtp` |  |  |

## app_group `gp292`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| tld-service | `svc_tld_service` |  |  |

## app_group `gp293`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-platon | `svc_remittance_platon` |  |  |

## app_group `gp294`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| exchange-rate-crawler | `svc_exchange_rate_crawler` |  |  |

## app_group `gp295`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| basis-portal | `svc_basis_portal` |  |  |

## app_group `gp296`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| gppc | `svc_gppc` |  |  |

## app_group `gp297`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| gppc-jaywan | `svc_gppc_jaywan` |  |  |

## app_group `gp298`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-trustbank | `svc_remittance_trustbank` |  |  |

## app_group `gp299`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-fawry | `svc_remittance_fawry` |  |  |

## app_group `gp300`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| basis-cas | `svc_basis_cas` |  |  |

## app_group `gp301`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-npss | `svc_qpay_npss` |  |  |

## app_group `gp302`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| gold-wallet | `svc_gold_wallet` |  |  |

## app_group `gp303`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-codepoint | `svc_remittance_codepoint` |  |  |

## app_group `gp304`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pns-merchant-mocker | `svc_pns_merchant_mocker` |  |  |

## app_group `gp307`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-cbe | `svc_remittance_cbe` |  |  |

## app_group `gp308`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| offline-payment | `svc_offline_payment` |  |  |

## app_group `gp311`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| tts | `svc_tts` |  |  |

## app_group `gp312`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| remittance-jinglepay | `svc_remittance_jinglepay` |  |  |

## app_group `gp313`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| qpay-zand | `svc_qpay_zand` |  |  |

## app_group `gp317`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| visii | `svc_visii` |  |  |

## app_group `gp318`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| fundchannel-mock | `svc_fundchannel_mock` |  |  |

## app_group `gp990`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| mock-ni | `svc_mock_ni` |  |  |

## app_group `gp997`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| jollychic-service | `svc_jollychic_service` |  |  |

## app_group `gt005`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cgs-apitest | `svc_cgs_apitest` |  |  |

## app_group `op002`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| cicd | `svc_cicd` |  |  |

## app_group `rt001`（4 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| promo-campaign | `svc_promo_campaign` |  |  |
| promo-engine | `svc_promo_engine` |  |  |
| promo-gateway | `svc_promo_gateway` |  |  |
| promo-merchant | `svc_promo_merchant` |  |  |

## app_group `rt002`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| afis | `svc_afis` |  |  |

## app_group `rt003`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| pqs | `svc_pqs` |  |  |

## app_group `rt004`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| palm-id | `svc_palm_id` |  |  |

## app_group `rt005`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| at-beb | `svc_at_beb` |  |  |

## app_group `rt006`（1 个）

| name | id | domain | owner |
| --- | --- | --- | --- |
| kiosk-mgmt | `svc_kiosk_mgmt` |  |  |

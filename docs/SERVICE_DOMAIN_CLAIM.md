# 服务认领表(可选 · 按需自取)

> 由 import_services.py + import_owners.py 生成。`当前域`=已分类的真实业务域(未分类=service-catalog)。
> `建议评审人`=Redis 迁移表里的 qa_tester(QA 同事,**仅线索**)。**认领=域负责人确认后**才把评审人正式落
> 进对象 owner/reviewer;知识 owner/reviewer 最终以 12 QA 域映射为准。`dev_owner`=开发联系人(已写进对象,排障参考)。

## app_group `(无)`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-arp | `svc_remittance_arp` | remittance |  |
| remittance-terrapay | `svc_remittance_terrapay` | remittance |  |

## app_group `bd002`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mysql-member-sync | `svc_mysql_member_sync` | service-catalog |  |

## app_group `bd004`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| data-server | `svc_data_server` | service-catalog |  |
| uae-data-server | `svc_uae_data_server` | service-catalog |  |

## app_group `bd006`（3）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| auth_server | `svc_auth_server` | service-catalog |  |
| crawl-leantech-server | `svc_crawl_leantech_server` | service-catalog |  |
| crawl-server | `svc_crawl_server` | service-catalog |  |

## app_group `bd007`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| feature-calculate-server | `svc_feature_calculate_server` | service-catalog |  |
| feature-calculate-server-new | `svc_feature_calculate_server_new` | service-catalog |  |

## app_group `gp001`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ues-ws | `svc_ues_ws` | service-catalog | 周晓妍 |

## app_group `gp002`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cmf | `svc_cmf` | payment-tools | 周晓妍 |
| cmf-task | `svc_cmf_task` | payment-tools |  |

## app_group `gp003`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pbs | `svc_pbs` | payment-tools | 周晓妍 |

## app_group `gp004`（3）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| dpm-accounting | `svc_dpm_accounting` | payment-core | 周晓妍 |
| dpm-manager | `svc_dpm_manager` | payment-core | 周晓妍 |
| dpm-task | `svc_dpm_task` | payment-core |  |

## app_group `gp005`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| member | `svc_member` | wallet | 谢跃男 |

## app_group `gp006`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| payment | `svc_payment` | payment-core | 周晓妍 |

## app_group `gp007`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cashdesk-api | `svc_cashdesk_api` | payment-core | 周晓妍 |

## app_group `gp008`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| acs | `svc_acs` | risk | 谢跃男 |

## app_group `gp009`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| voucher | `svc_voucher` | service-catalog | 周晓妍 |

## app_group `gp011`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| deposit | `svc_deposit` | service-catalog |  |

## app_group `gp012`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| fundout | `svc_fundout` | online-business |  |

## app_group `gp013`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pns | `svc_pns` | service-catalog | 谢跃男 |

## app_group `gp014`（3）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pfs-basis | `svc_pfs_basis` | service-catalog | 谢跃男 |
| pfs-manager | `svc_pfs_manager` | service-catalog | 谢跃男 |
| pfs-payment | `svc_pfs_payment` | payment-core | 周晓妍 |

## app_group `gp016`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| outman | `svc_outman` | service-catalog | 谢跃男 |

## app_group `gp018`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| spring-boot-admin | `svc_spring_boot_admin` | service-catalog |  |

## app_group `gp019`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| spring-cloud-config | `svc_spring_cloud_config` | service-catalog |  |

## app_group `gp020`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| dubbo-admin | `svc_dubbo_admin` | service-catalog |  |

## app_group `gp021`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| elasticjob-console | `svc_elasticjob_console` | service-catalog |  |

## app_group `gp022`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| software-management | `svc_software_management` | service-catalog | 王粲 |

## app_group `gp023`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| basis | `svc_basis` | portal-operations | 谢跃男 |

## app_group `gp024`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cgs | `svc_cgs` | wallet | 周晓妍 |

## app_group `gp026`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pos-gateway | `svc_pos_gateway` | offline-business | 王粲 |

## app_group `gp028`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| sgs | `svc_sgs` | online-business | 周晓妍 |

## app_group `gp030`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| query | `svc_query` | service-catalog | 周晓妍 |
| query-datasync | `svc_query_datasync` | service-catalog | 谢跃男 |

## app_group `gp031`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| counter | `svc_counter` | payment-tools | 谢跃男 |

## app_group `gp032`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| personal | `svc_personal` | wallet | 谢跃男 |

## app_group `gp033`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| xbh-gateway | `svc_xbh_gateway` | service-catalog | 王粲 |

## app_group `gp034`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| authpay | `svc_authpay` | service-catalog | 周晓妍 |

## app_group `gp035`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| socialpay | `svc_socialpay` | service-catalog | 谢跃男 |

## app_group `gp037`（3）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mns-listener | `svc_mns_listener` | service-catalog |  |
| mns-main | `svc_mns_main` | service-catalog |  |
| mns-scheduler | `svc_mns_scheduler` | service-catalog |  |

## app_group `gp038`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| bigdata-admin | `svc_bigdata_admin` | service-catalog | 谢跃男 |
| bigdata-ws | `svc_bigdata_ws` | service-catalog | 谢跃男 |

## app_group `gp039`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| fcw | `svc_fcw` | service-catalog |  |

## app_group `gp040`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pts | `svc_pts` | service-catalog | 谢跃男 |

## app_group `gp041`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pbs-bos | `svc_pbs_bos` | service-catalog |  |

## app_group `gp042`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pcs | `svc_pcs` | service-catalog | 谢跃男 |

## app_group `gp043`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| reconciliation | `svc_reconciliation` | payment-tools | 谢跃男 |

## app_group `gp044`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| merchant | `svc_merchant` | portal-operations |  |

## app_group `gp045`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| merchant-console-frontend | `svc_merchant_console_frontend` | service-catalog | 谢跃男 |

## app_group `gp046`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pcm | `svc_pcm` | service-catalog | 周晓妍 |

## app_group `gp047`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ppcenter | `svc_ppcenter` | payment-tools | 谢跃男 |

## app_group `gp048`（10）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| hive-activities | `svc_hive_activities` | service-catalog |  |
| hive-bank-console | `svc_hive_bank_console` | service-catalog |  |
| hive-cashier | `svc_hive_cashier` | service-catalog |  |
| hive-checkout | `svc_hive_checkout` | service-catalog |  |
| hive-developers | `svc_hive_developers` | service-catalog |  |
| hive-m-topay | `svc_hive_m_topay` | service-catalog |  |
| hive-mcashier | `svc_hive_mcashier` | service-catalog |  |
| hive-merchant-console | `svc_hive_merchant_console` | service-catalog |  |
| hive-portal | `svc_hive_portal` | service-catalog |  |
| hive-utilities | `svc_hive_utilities` | service-catalog |  |

## app_group `gp050`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cps | `svc_cps` | service-catalog | 谢跃男 |

## app_group `gp053`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| transfer | `svc_transfer` | service-catalog | 谢跃男 |

## app_group `gp054`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| device | `svc_device` | offline-business | 谢跃男 |

## app_group `gp055`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| sqlmonitor | `svc_sqlmonitor` | service-catalog |  |

## app_group `gp056`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| csc | `svc_csc` | service-catalog |  |

## app_group `gp057`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| fido-mgmt | `svc_fido_mgmt` | service-catalog |  |
| fidoservice | `svc_fidoservice` | service-catalog |  |

## app_group `gp058`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cash-eatm | `svc_cash_eatm` | service-catalog | 王粲 |

## app_group `gp060`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| authorization-service | `svc_authorization_service` | service-catalog | 谢跃男 |

## app_group `gp062`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| h2h | `svc_h2h` | service-catalog | 谢跃男 |

## app_group `gp064`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| customer-frontend | `svc_customer_frontend` | service-catalog | 谢跃男 |

## app_group `gp065`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| porter | `svc_porter` | service-catalog |  |

## app_group `gp066`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| channel-mobile-ding | `svc_channel_mobile_ding` | service-catalog |  |

## app_group `gp068`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| marketing | `svc_marketing` | payment-tools | 谢跃男 |

## app_group `gp069`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| acquireii | `svc_acquireii` | online-business | 王粲 |

## app_group `gp070`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| csimple | `svc_csimple` | service-catalog | 谢跃男 |

## app_group `gp071`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| merchant-frontend | `svc_merchant_frontend` | portal-operations | 谢跃男 |

## app_group `gp073`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| supplier | `svc_supplier` | service-catalog | 谢跃男 |

## app_group `gp074`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| life-center | `svc_life_center` | service-catalog | 周晓妍 |

## app_group `gp075`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| market-goods | `svc_market_goods` | service-catalog | 周晓妍 |

## app_group `gp076`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| market-order | `svc_market_order` | service-catalog | 周晓妍 |

## app_group `gp077`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| user-profile-scheduler | `svc_user_profile_scheduler` | service-catalog |  |

## app_group `gp078`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| kyc | `svc_kyc` | kyc | 谢跃男 |

## app_group `gp079`（4）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| grc-check-identity-provider | `svc_grc_check_identity_provider` | risk | 周晓妍 |
| grc-component-connect-provider | `svc_grc_component_connect_provider` | risk | 周晓妍 |
| grc-cps-provider | `svc_grc_cps_provider` | risk |  |
| grc-engine-provider | `svc_grc_engine_provider` | risk | 谢跃男 |

## app_group `gp080`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cqm | `svc_cqm` | service-catalog | 张萌萌 |

## app_group `gp081`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cbm | `svc_cbm` | service-catalog | 张萌萌 |

## app_group `gp083`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| merchant-fundout | `svc_merchant_fundout` | service-catalog | 王粲 |

## app_group `gp084`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| otpmock | `svc_otpmock` | service-catalog |  |
| otps | `svc_otps` | service-catalog | 周晓妍 |

## app_group `gp085`（7）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| oauth-client-service-cgs-impl | `svc_oauth_client_service_cgs_impl` | service-catalog |  |
| resource-service-cgs-impl | `svc_resource_service_cgs_impl` | service-catalog |  |
| resource-service-rpc-dubbo-provider | `svc_resource_service_rpc_dubbo_provider` | service-catalog | 谢跃男 |
| resource-service-sgs-impl | `svc_resource_service_sgs_impl` | service-catalog |  |
| resource-service-web | `svc_resource_service_web` | service-catalog | 谢跃男 |
| session-service-cgs-impl | `svc_session_service_cgs_impl` | service-catalog | 谢跃男 |
| session-service-rpc-dubbo-provider | `svc_session_service_rpc_dubbo_provider` | service-catalog | 谢跃男 |

## app_group `gp086`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cbs | `svc_cbs` | service-catalog | 周晓妍 |

## app_group `gp087`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-mcii | `svc_qpay_mcii` | payment-tools | 谢跃男 |

## app_group `gp088`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-fs | `svc_qpay_fs` | payment-tools |  |

## app_group `gp089`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| agreements-static | `svc_agreements_static` | service-catalog |  |

## app_group `gp091`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cms | `svc_cms` | service-catalog |  |

## app_group `gp092`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-pl-channel | `svc_qpay_pl_channel` | payment-tools |  |

## app_group `gp093`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cards | `svc_cards` | card | 周晓妍 |

## app_group `gp094`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| basis-cms | `svc_basis_cms` | service-catalog | 周晓妍 |

## app_group `gp095`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| paylater | `svc_paylater` | service-catalog | 张萌萌 |

## app_group `gp096`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| css | `svc_css` | service-catalog | 谢跃男 |

## app_group `gp098`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| green-points | `svc_green_points` | service-catalog |  |

## app_group `gp099`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| gpoint | `svc_gpoint` | service-catalog | 周晓妍 |

## app_group `gp100`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ons | `svc_ons` | service-catalog | 周晓妍 |

## app_group `gp101`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| authorization-token | `svc_authorization_token` | service-catalog | 王粲 |

## app_group `gp103`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| kiosk-channel | `svc_kiosk_channel` | service-catalog |  |

## app_group `gp104`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| escrow | `svc_escrow` | service-catalog | 谢跃男 |

## app_group `gp105`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| marketing-event | `svc_marketing_event` | service-catalog | 谢跃男 |

## app_group `gp106`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| iso8583-gateway | `svc_iso8583_gateway` | service-catalog |  |

## app_group `gp107`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| contract | `svc_contract` | service-catalog |  |

## app_group `gp110`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| gptrade | `svc_gptrade` | service-catalog | 谢跃男 |

## app_group `gp114`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ufs2 | `svc_ufs2` | service-catalog | 周晓妍 |

## app_group `gp116`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| shortlink | `svc_shortlink` | service-catalog |  |

## app_group `gp120`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| protocol | `svc_protocol` | service-catalog | 谢跃男 |
| protocol-duplicate | `svc_protocol_duplicate` | service-catalog | 谢跃男 |

## app_group `gp122`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| invoice | `svc_invoice` | service-catalog |  |

## app_group `gp123`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| tradeii | `svc_tradeii` | payment-core | 周晓妍 |

## app_group `gp124`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| router | `svc_router` | payment-tools |  |

## app_group `gp125`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| adtaxi | `svc_adtaxi` | service-catalog | 谢跃男 |

## app_group `gp126`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cmsii | `svc_cmsii` | service-catalog | 周晓妍 |

## app_group `gp127`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mcs | `svc_mcs` | service-catalog |  |

## app_group `gp129`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| channel-paykii | `svc_channel_paykii` | service-catalog |  |

## app_group `gp130`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| credit-business | `svc_credit_business` | service-catalog | 张萌萌 |

## app_group `gp131`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| marketnotify | `svc_marketnotify` | service-catalog |  |

## app_group `gp133`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| vcs | `svc_vcs` | service-catalog |  |

## app_group `gp134`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| statementii | `svc_statementii` | service-catalog |  |

## app_group `gp135`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| member-front | `svc_member_front` | wallet | 谢跃男 |

## app_group `gp136`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| custom | `svc_custom` | service-catalog | 周晓妍 |

## app_group `gp137`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| asset-info | `svc_asset_info` | service-catalog | 谢跃男 |

## app_group `gp138`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| crypto-currency-exchange | `svc_crypto_currency_exchange` | service-catalog | 谢跃男 |

## app_group `gp139`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| facepay-api | `svc_facepay_api` | service-catalog |  |

## app_group `gp140`（3）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ccdpm-accounting | `svc_ccdpm_accounting` | payment-core | 周晓妍 |
| ccdpm-manager | `svc_ccdpm_manager` | payment-core | 周晓妍 |
| ccdpm-task | `svc_ccdpm_task` | payment-core |  |

## app_group `gp141`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mssii | `svc_mssii` | service-catalog | 谢跃男 |

## app_group `gp142`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| quotation | `svc_quotation` | service-catalog | 谢跃男 |

## app_group `gp144`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| holding | `svc_holding` | service-catalog | 谢跃男 |

## app_group `gp145`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-sales | `svc_cc_sales` | service-catalog | 谢跃男 |

## app_group `gp146`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-withdraw | `svc_cc_withdraw` | service-catalog | 谢跃男 |

## app_group `gp148`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| member-feature | `svc_member_feature` | wallet | 谢跃男 |

## app_group `gp149`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| vis | `svc_vis` | service-catalog | 谢跃男 |

## app_group `gp150`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| host | `svc_host` | service-catalog | 谢跃男 |

## app_group `gp151`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| host-gateway | `svc_host_gateway` | service-catalog | 谢跃男 |

## app_group `gp153`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| upic | `svc_upic` | service-catalog | 谢跃男 |

## app_group `gp154`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-channel-eth | `svc_cc_channel_eth` | service-catalog | 王粲 |

## app_group `gp155`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-deposit | `svc_cc_deposit` | service-catalog | 王粲 |

## app_group `gp156`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| exchange | `svc_exchange` | payment-tools |  |

## app_group `gp158`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-installment | `svc_qpay_installment` | payment-tools |  |

## app_group `gp159`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-channel-btc | `svc_cc_channel_btc` | service-catalog | 王粲 |

## app_group `gp160`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| comp-service | `svc_comp_service` | service-catalog | 谢跃男 |

## app_group `gp161`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| basis-merchant | `svc_basis_merchant` | portal-operations | 谢跃男 |

## app_group `gp162`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-transfer | `svc_cc_transfer` | service-catalog | 谢跃男 |

## app_group `gp163`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| coupon | `svc_coupon` | service-catalog | 谢跃男 |

## app_group `gp164`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| coupon-service | `svc_coupon_service` | service-catalog | 谢跃男 |

## app_group `gp165`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| coupon-gateway | `svc_coupon_gateway` | service-catalog | 谢跃男 |

## app_group `gp170`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-trade | `svc_cc_trade` | service-catalog | 谢跃男 |

## app_group `gp176`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-cashier | `svc_cc_cashier` | service-catalog | 周晓妍 |

## app_group `gp178`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| calculator | `svc_calculator` | service-catalog | 谢跃男 |

## app_group `gp180`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-acquire | `svc_cc_acquire` | service-catalog | 谢跃男 |

## app_group `gp181`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cc-channel-tron | `svc_cc_channel_tron` | service-catalog | 王粲 |

## app_group `gp184`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| df-calculation | `svc_df_calculation` | service-catalog |  |

## app_group `gp185`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| gadget | `svc_gadget` | service-catalog | 谢跃男 |

## app_group `gp186`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| 3ds2 | `svc_3ds2` | service-catalog |  |

## app_group `gp187`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-ni-channel | `svc_qpay_ni_channel` | payment-tools |  |

## app_group `gp188`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance | `svc_remittance` | remittance | 谢跃男 |

## app_group `gp189`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| marketing-campaign | `svc_marketing_campaign` | service-catalog | 谢跃男 |

## app_group `gp190`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| marketing-gateway | `svc_marketing_gateway` | service-catalog | 谢跃男 |

## app_group `gp192`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| fraud | `svc_fraud` | risk | 谢跃男 |

## app_group `gp193`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cashierii | `svc_cashierii` | payment-core | 周晓妍 |

## app_group `gp194`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| basis-customer | `svc_basis_customer` | service-catalog | 谢跃男 |

## app_group `gp195`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| tpay-nyu | `svc_tpay_nyu` | service-catalog |  |

## app_group `gp197`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| preauth | `svc_preauth` | service-catalog | 王粲 |

## app_group `gp199`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cloud-mis | `svc_cloud_mis` | service-catalog |  |

## app_group `gp200`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-fsii | `svc_qpay_fsii` | payment-tools |  |

## app_group `gp201`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-klip | `svc_qpay_klip` | payment-tools |  |

## app_group `gp202`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| kyc-service | `svc_kyc_service` | kyc | 谢跃男 |

## app_group `gp204`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| data-etl | `svc_data_etl` | service-catalog |  |

## app_group `gp205`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| deduct | `svc_deduct` | service-catalog | 王粲 |

## app_group `gp207`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| das | `svc_das` | service-catalog | 谢跃男 |

## app_group `gp209`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| aml | `svc_aml` | compliance |  |

## app_group `gp210`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| npss-gateway | `svc_npss_gateway` | service-catalog | 谢跃男 |

## app_group `gp212`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ppc | `svc_ppc` | service-catalog | 剑飞 |

## app_group `gp213`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pos-exception-processor | `svc_pos_exception_processor` | service-catalog | 王粲 |

## app_group `gp216`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| rdgs | `svc_rdgs` | service-catalog | 谢跃男 |

## app_group `gp220`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| youstore-installment | `svc_youstore_installment` | service-catalog |  |

## app_group `gp221`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-cko | `svc_qpay_cko` | payment-tools |  |

## app_group `gp222`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| npss | `svc_npss` | service-catalog | 谢跃男 |

## app_group `gp223`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mock-datawire | `svc_mock_datawire` | service-catalog |  |

## app_group `gp225`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| asite | `svc_asite` | service-catalog |  |

## app_group `gp227`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| push-to-pay | `svc_push_to_pay` | service-catalog |  |

## app_group `gp230`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pus | `svc_pus` | service-catalog |  |

## app_group `gp231`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| escrowii | `svc_escrowii` | service-catalog |  |

## app_group `gp232`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-aplus | `svc_qpay_aplus` | payment-tools | 谢跃男 |

## app_group `gp233`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| leanlink | `svc_leanlink` | service-catalog | 谢跃男 |

## app_group `gp234`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-lean | `svc_qpay_lean` | payment-tools |  |

## app_group `gp236`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| wechat-channel | `svc_wechat_channel` | service-catalog | 谢跃男 |

## app_group `gp237`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| payroll-core-service | `svc_payroll_core_service` | wps |  |

## app_group `gp238`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ifb-channel | `svc_ifb_channel` | service-catalog | 谢跃男 |

## app_group `gp239`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| feebill | `svc_feebill` | service-catalog | 剑飞 |

## app_group `gp240`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| household | `svc_household` | service-catalog | 金华 |

## app_group `gp242`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| corporate-portal | `svc_corporate_portal` | service-catalog |  |

## app_group `gp243`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mock-channel | `svc_mock_channel` | service-catalog |  |

## app_group `gp244`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-nipos | `svc_qpay_nipos` | payment-tools |  |

## app_group `gp245`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-fts | `svc_qpay_fts` | payment-tools | 谢跃男 |

## app_group `gp247`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| datasavvy | `svc_datasavvy` | service-catalog | 谢跃男 |

## app_group `gp251`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| unified-merchant-portal | `svc_unified_merchant_portal` | service-catalog |  |

## app_group `gp252`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-nisocket | `svc_qpay_nisocket` | payment-tools |  |

## app_group `gp254`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| onboarding | `svc_onboarding` | portal-operations |  |

## app_group `gp257`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-swiftx | `svc_remittance_swiftx` | remittance |  |

## app_group `gp258`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| crs | `svc_crs` | service-catalog |  |

## app_group `gp259`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cregister | `svc_cregister` | service-catalog |  |

## app_group `gp261`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pix | `svc_pix` | service-catalog |  |

## app_group `gp262`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-niboarding | `svc_qpay_niboarding` | payment-tools |  |

## app_group `gp264`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-bdo | `svc_remittance_bdo` | remittance |  |

## app_group `gp267`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-mpgs | `svc_qpay_mpgs` | payment-tools |  |

## app_group `gp268`（2）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| bigdata-router | `svc_bigdata_router` | service-catalog |  |
| bigdata-router-admin | `svc_bigdata_router_admin` | service-catalog |  |

## app_group `gp269`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-enbd | `svc_qpay_enbd` | payment-tools |  |

## app_group `gp270`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| member-task | `svc_member_task` | wallet |  |

## app_group `gp274`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| bafl-channel | `svc_bafl_channel` | service-catalog |  |

## app_group `gp275`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| acquire2-query | `svc_acquire2_query` | service-catalog |  |

## app_group `gp276`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-ime | `svc_remittance_ime` | remittance |  |

## app_group `gp278`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| customer-service | `svc_customer_service` | service-catalog |  |

## app_group `gp279`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| commission | `svc_commission` | service-catalog |  |

## app_group `gp280`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| ni-mock | `svc_ni_mock` | service-catalog |  |

## app_group `gp281`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| officer | `svc_officer` | service-catalog |  |

## app_group `gp283`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pcbs | `svc_pcbs` | service-catalog |  |

## app_group `gp284`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pws | `svc_pws` | service-catalog |  |

## app_group `gp286`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| adg | `svc_adg` | service-catalog |  |

## app_group `gp287`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-ext | `svc_remittance_ext` | remittance |  |

## app_group `gp288`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| merchant-settlement | `svc_merchant_settlement` | service-catalog |  |

## app_group `gp289`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cns | `svc_cns` | service-catalog |  |

## app_group `gp290`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-fuze | `svc_remittance_fuze` | remittance |  |

## app_group `gp291`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| rtp | `svc_rtp` | service-catalog |  |

## app_group `gp292`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| tld-service | `svc_tld_service` | service-catalog |  |

## app_group `gp293`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-platon | `svc_remittance_platon` | remittance |  |

## app_group `gp294`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| exchange-rate-crawler | `svc_exchange_rate_crawler` | service-catalog |  |

## app_group `gp295`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| basis-portal | `svc_basis_portal` | service-catalog |  |

## app_group `gp296`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| gppc | `svc_gppc` | service-catalog |  |

## app_group `gp297`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| gppc-jaywan | `svc_gppc_jaywan` | service-catalog |  |

## app_group `gp298`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-trustbank | `svc_remittance_trustbank` | remittance |  |

## app_group `gp299`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-fawry | `svc_remittance_fawry` | remittance |  |

## app_group `gp300`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| basis-cas | `svc_basis_cas` | service-catalog |  |

## app_group `gp301`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-npss | `svc_qpay_npss` | payment-tools |  |

## app_group `gp302`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| gold-wallet | `svc_gold_wallet` | service-catalog |  |

## app_group `gp303`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-codepoint | `svc_remittance_codepoint` | remittance |  |

## app_group `gp304`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pns-merchant-mocker | `svc_pns_merchant_mocker` | service-catalog |  |

## app_group `gp307`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-cbe | `svc_remittance_cbe` | remittance |  |

## app_group `gp308`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| offline-payment | `svc_offline_payment` | service-catalog |  |

## app_group `gp311`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| tts | `svc_tts` | service-catalog |  |

## app_group `gp312`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| remittance-jinglepay | `svc_remittance_jinglepay` | remittance |  |

## app_group `gp313`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| qpay-zand | `svc_qpay_zand` | payment-tools |  |

## app_group `gp317`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| visii | `svc_visii` | service-catalog |  |

## app_group `gp318`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| fundchannel-mock | `svc_fundchannel_mock` | service-catalog |  |

## app_group `gp990`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| mock-ni | `svc_mock_ni` | service-catalog |  |

## app_group `gp997`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| jollychic-service | `svc_jollychic_service` | service-catalog | 王粲 |

## app_group `gt005`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cgs-apitest | `svc_cgs_apitest` | service-catalog |  |

## app_group `op002`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| cicd | `svc_cicd` | service-catalog |  |

## app_group `rt001`（4）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| promo-campaign | `svc_promo_campaign` | service-catalog |  |
| promo-engine | `svc_promo_engine` | service-catalog |  |
| promo-gateway | `svc_promo_gateway` | service-catalog |  |
| promo-merchant | `svc_promo_merchant` | service-catalog |  |

## app_group `rt002`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| afis | `svc_afis` | service-catalog |  |

## app_group `rt003`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| pqs | `svc_pqs` | service-catalog | 谢跃男 |

## app_group `rt004`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| palm-id | `svc_palm_id` | service-catalog |  |

## app_group `rt005`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| at-beb | `svc_at_beb` | service-catalog |  |

## app_group `rt006`（1）

| 服务 | id | 当前域 | 建议评审人(qa_tester) |
| --- | --- | --- | --- |
| kiosk-mgmt | `svc_kiosk_mgmt` | service-catalog |  |

### [Index](https://github.com/PaaS-TA/Guide) > [User Guide](user_guide.md) > Monitoring MariaDB


# Monitoring MariaDB User Guide
1. [개요](#1)
2. [Monitoring MariaDB 테이블/컬럼 명세](#2)


## <div id="1">1. 개요
이 문서는 PaaS-TA Monitoring Dashboard 배포시 생성되는 mariadb VM 내 설치된 MariaDB의 데이터베이스와 테이블/컬럼 구조에 대한 명세와 가이드를 제공하기 위해 작성되었다.


## <div id="2">2. Monitoring MariaDB 테이블/컬럼 명세
### 2.1. PaastaMonitoring
**![](images/table.png) alarm_actions**  
: 발생한 알람에 대한 관리자의 조치 이력을 관리한다.

| Column                                   | Properties                     |
|------------------------------------------|--------------------------------|
| ![](images/primary-column.png) id        | int unsigned (auto increment)  |
| ![](images/column.png) alarm_id          | int                            |
| ![](images/column.png) alarm_action_desc | text                           |
| ![](images/column.png) reg_date          | datetime = current_timestamp() |
| ![](images/column.png) reg_user          | varchar(36) = 'system'         |
| ![](images/column.png) modi_date         | datetime = current_timestamp() |
| ![](images/column.png) modi_user         | varchar(36) = 'system'         |

**![](images/table.png) alarm_policies**  
: 알람 임계치 정책(기준)을 관리한다.

| Column                                    | Properties                     |
|-------------------------------------------|--------------------------------|
| ![](images/primary-column.png) id         | int unsigned (auto increment)  |
| ![](images/column.png) origin_type        | varchar(3)                     |
| ![](images/column.png) alarm_type         | varchar(6)                     |
| ![](images/column.png) warning_threshold  | int                            |
| ![](images/column.png) critical_threshold | int                            |
| ![](images/column.png) repeat_time        | int                            |
| ![](images/column.png) measure_time       | int                            |
| ![](images/column.png) comment            | varchar(5000)                  |
| ![](images/column.png) reg_date           | datetime = current_timestamp() |
| ![](images/column.png) reg_user           | varchar(36) = 'system'         |
| ![](images/column.png) modi_date          | datetime = current_timestamp() |
| ![](images/column.png) modi_user          | varchar(36) = 'system'         |

**![](images/table.png) alarm_sns**  
: 알람 발생시 알림 받을 SNS 채널(Telegram)을 관리한다.

| Column                                    | Properties                     |
|-------------------------------------------|--------------------------------|
| ![](images/primary-column.png) channel_id | int unsigned (auto increment)  |
| ![](images/column.png) origin_type        | varchar(3) = 'all'             |
| ![](images/column.png) sns_type           | varchar(50)                    |
| ![](images/column.png) sns_id             | varchar(50)                    |
| ![](images/column.png) token              | varchar(300)                   |
| ![](images/column.png) expl               | varchar(100)                   |
| ![](images/column.png) sns_send_yn        | varchar(1) = 'Y'               |
| ![](images/column.png) reg_date           | datetime = current_timestamp() |
| ![](images/column.png) reg_user           | varchar(36) = 'system'         |
| ![](images/column.png) modi_date          | datetime = current_timestamp() |
| ![](images/column.png) modi_user          | varchar(36) = 'system'         |

**![](images/table.png) alarm_sns_targets**  
: 알람 발생시 알림 받을 SNS 채널(Telegram)의 사용자 번호를 관리한다.

| Column                            | Properties                     |
|-----------------------------------|--------------------------------|
| ![](images/column.png) channel_id | int unsigned                   |
| ![](images/column.png) target_id  | bigint unsigned                |
| ![](images/column.png) reg_date   | datetime = current_timestamp() |
| ![](images/column.png) reg_user   | varchar(36) = 'system'         |
| ![](images/column.png) modi_date  | datetime = current_timestamp() |
| ![](images/column.png) modi_user  | varchar(36) = 'system'         |

**![](images/table.png) alarm_targets**  
: 알람 발생시 알림 받을 이메일을 관리한다.

| Column                              | Properties                     |
|-------------------------------------|--------------------------------|
| ![](images/primary-column.png) id   | int unsigned (auto increment)  |
| ![](images/column.png) origin_type  | varchar(3)                     |
| ![](images/column.png) mail_address | varchar(100)                   |
| ![](images/column.png) mail_send_yn | varchar(1) = 'Y'               |
| ![](images/column.png) reg_date     | datetime = current_timestamp() |
| ![](images/column.png) reg_user     | varchar(36) = 'system'         |
| ![](images/column.png) modi_date    | datetime = current_timestamp() |
| ![](images/column.png) modi_user    | varchar(36) = 'system'         |

**![](images/table.png) alarms**  
: 발생된 알람 이력을 관리한다.

| Column                                 | Properties                     |
|----------------------------------------|--------------------------------|
| ![](images/primary-column.png) id      | int unsigned (auto increment)  |
| ![](images/column.png) origin_type     | varchar(3)                     |
| ![](images/column.png) origin_id       | int                            |
| ![](images/column.png) alarm_type      | varchar(6)                     |
| ![](images/column.png) level           | varchar(8)                     |
| ![](images/column.png) ip              | varchar(15)                    |
| ![](images/column.png) app_yn          | varchar(1)                     |
| ![](images/column.png) app_name        | varchar(500)                   |
| ![](images/column.png) app_index       | int                            |
| ![](images/column.png) container_name  | varchar(40)                    |
| ![](images/column.png) alarm_title     | varchar(5000)                  |
| ![](images/column.png) alarm_message   | text                           |
| ![](images/column.png) resolve_status  | varchar(1)                     |
| ![](images/column.png) alarm_cnt       | int = 1                        |
| ![](images/column.png) reg_date        | datetime = current_timestamp() |
| ![](images/column.png) reg_user        | varchar(36) = 'system'         |
| ![](images/column.png) modi_date       | datetime = current_timestamp() |
| ![](images/column.png) modi_user       | varchar(36) = 'system'         |
| ![](images/column.png) alarm_send_date | datetime                       |
| ![](images/column.png) complete_date   | datetime                       |
| ![](images/column.png) complete_user   | varchar(36)                    |

**![](images/table.png) app_alarm_histories**  
: 애플리케이션에서 발생한 알람 이력을 관리한다.

| Column                                     | Properties                     |
|--------------------------------------------|--------------------------------|
| ![](images/primary-column.png) alarm_id    | int unsigned                   |
| ![](images/column.png) app_guid            | varchar(50)                    |
| ![](images/column.png) app_idx             | int unsigned                   |
| ![](images/column.png) resource_type       | varchar(10)                    |
| ![](images/column.png) alarm_level         | varchar(8)                     |
| ![](images/column.png) app_name            | varchar(50)                    |
| ![](images/column.png) cell_ip             | varchar(15)                    |
| ![](images/column.png) container_id        | varchar(50)                    |
| ![](images/column.png) container_interface | varchar(20)                    |
| ![](images/column.png) alarm_title         | varchar(1000)                  |
| ![](images/column.png) alarm_message       | text                           |
| ![](images/column.png) alarm_send_date     | datetime                       |
| ![](images/column.png) terminate_yn        | varchar(1)                     |
| ![](images/column.png) reg_date            | datetime = current_timestamp() |
| ![](images/column.png) reg_user            | varchar(36) = 'system'         |
| ![](images/column.png) modi_date           | datetime = current_timestamp() |
| ![](images/column.png) modi_user           | varchar(36) = 'system'         |

**![](images/table.png) app_alarm_policies**  
: 애플리케이션의 알람 임계치 정책(기준)을 관리한다.

| Column                                           | Properties                     |
|--------------------------------------------------|--------------------------------|
| ![](images/primary-column.png) app_guid          | varchar(50)                    |
| ![](images/column.png) cpu_warning_threshold     | int unsigned                   |
| ![](images/column.png) cpu_critical_threshold    | int unsigned                   |
| ![](images/column.png) memory_warning_threshold  | int unsigned                   |
| ![](images/column.png) memory_critical_threshold | int unsigned                   |
| ![](images/column.png) measure_time_sec          | int unsigned                   |
| ![](images/column.png) email                     | varchar(100)                   |
| ![](images/column.png) email_send_yn             | varchar(1)                     |
| ![](images/column.png) alarm_use_yn              | varchar(1)                     |
| ![](images/column.png) reg_date                  | datetime = current_timestamp() |
| ![](images/column.png) reg_user                  | varchar(36) = 'system'         |
| ![](images/column.png) modi_date                 | datetime = current_timestamp() |
| ![](images/column.png) modi_user                 | varchar(36) = 'system'         |

**![](images/table.png) app_auto_scaling_policies**  
: 애플리케이션의 오토스케일 정책(기준)을 관리한다.

| Column                                        | Properties                     |
|-----------------------------------------------|--------------------------------|
| ![](images/primary-column.png) app_guid       | varchar(50)                    |
| ![](images/column.png) instance_min_cnt       | int unsigned                   |
| ![](images/column.png) instance_max_cnt       | int unsigned                   |
| ![](images/column.png) cpu_min_threshold      | int unsigned                   |
| ![](images/column.png) cpu_max_threshold      | int unsigned                   |
| ![](images/column.png) memory_min_threshold   | int unsigned                   |
| ![](images/column.png) memory_max_threshold   | int unsigned                   |
| ![](images/column.png) instance_scaling_unit  | int unsigned                   |
| ![](images/column.png) measure_time_sec       | int unsigned                   |
| ![](images/column.png) auto_scaling_cpu_yn    | varchar(1)                     |
| ![](images/column.png) auto_scaling_memory_yn | varchar(1)                     |
| ![](images/column.png) auto_scaling_out_yn    | varchar(1)                     |
| ![](images/column.png) auto_scaling_in_yn     | varchar(1)                     |
| ![](images/column.png) reg_date               | datetime = current_timestamp() |
| ![](images/column.png) reg_user               | varchar(36) = 'system'         |
| ![](images/column.png) modi_date              | datetime = current_timestamp() |
| ![](images/column.png) modi_user              | varchar(36) = 'system'         |

**![](images/table.png) batch_alarm_executions_resolves**  
: (확인중)

| Column                                    | Properties                        |
|-------------------------------------------|-----------------------------------|
| ![](images/primary-column.png) resolve_id | bigint unsignded (auto increment) |
| ![](images/column.png) excution_id        | bigint                            |
| ![](images/column.png) alarm_action_desc  | varchar(4000)                     |
| ![](images/column.png) reg_date           | datetime                          |

**![](images/table.png) batch_alarm_executions**  
: (확인중)

| Column                                     | Properties                       |
|--------------------------------------------|----------------------------------|
| ![](images/primary-column.png) excution_id | bigint unsigned (auto increment) |
| ![](images/column.png) alarm_id            | int                              |
| ![](images/column.png) service_type        | varchar(10)                      |
| ![](images/column.png) critical_status     | varchar(50)                      |
| ![](images/column.png) measure_value       | float                            |
| ![](images/column.png) measure_name1       | varchar(200)                     |
| ![](images/column.png) measure_name2       | varchar(200)                     |
| ![](images/column.png) measure_name3       | varchar(200)                     |
| ![](images/column.png) execution_time      | timestamp = current_timestamp()  |
| ![](images/column.png) execution_result    | varchar(1000)                    |
| ![](images/column.png) resolve_status      | varchar(1)                       |
| ![](images/column.png) complete_date       | datetime                         |

**![](images/table.png) batch_alarm_infos**  
: (확인중)

| Column                                  | Properties                       |
|-----------------------------------------|----------------------------------|
| ![](images/primary-column.png) alarm_id | bigint unsigned (auto increment) |
| ![](images/column.png) service_type     | varchar(10)                      |
| ![](images/column.png) metric_type      | varchar(50)                      |
| ![](images/column.png) warning_value    | int                              |
| ![](images/column.png) critical_value   | int                              |
| ![](images/column.png) measure_time     | int                              |
| ![](images/column.png) cron_expression  | varchar(50)                      |
| ![](images/column.png) exec_msg         | varchar(1000)                    |
| ![](images/column.png) param_data1      | varchar(1000)                    |
| ![](images/column.png) param_data2      | varchar(1000)                    |
| ![](images/column.png) param_data3      | varchar(1000)                    |

**![](images/table.png) batch_alarm_receivers**  
: (확인중)

| Column                                     | Properties                     |
|--------------------------------------------|--------------------------------|
| ![](images/primary-column.png) receiver_id | int unsigned (auto increment)  |
| ![](images/column.png) service_type        | varchar(10)                    |
| ![](images/column.png) receive_type        | varchar(100)                   |
| ![](images/column.png) target_id           | varchar(200)                   |
| ![](images/column.png) use_yn              | varchar(1) = 'Y'               |
| ![](images/column.png) reg_date            | datetime = current_timestamp() |
| ![](images/column.png) reg_user            | varchar(36) = 'system'         |
| ![](images/column.png) modi_date           | datetime = current_timestamp() |
| ![](images/column.png) modi_user           | varchar(36) = 'system'         |

**![](images/table.png) batch_alarm_sns**  
: (확인중)

| Column                                    | Properties                       |
|-------------------------------------------|----------------------------------|
| ![](images/primary-column.png) channel_id | bigint unsigned (auto increment) |
| ![](images/column.png) origin_type        | varchar(10)                      |
| ![](images/column.png) sns_id             | varchar(200)                     |
| ![](images/column.png) token              | varchar(1000)                    |
| ![](images/column.png) expl               | varchar(100)                     |
| ![](images/column.png) sns_send_yn        | varchar(1) = 'Y'                 |
| ![](images/column.png) reg_date           | datetime = current_timestamp()   |
| ![](images/column.png) reg_user           | varchar(36) = 'system'           |
| ![](images/column.png) modi_date          | datetime = current_timestamp()   |
| ![](images/column.png) modi_user          | varchar(36) = 'system'           |

**![](images/table.png) member_infos**  
: Monitoring Dashboard 유저 정보를 관리한다.

| Column                                  | Properties                     |
|-----------------------------------------|--------------------------------|
| ![](images/primary-column.png) user_id  | varchar(50)                    |
| ![](images/column.png) user_pw          | varchar(500)                   |
| ![](images/column.png) user_email       | varchar(100)                   |
| ![](images/column.png) user_nm          | varchar(100)                   |
| ![](images/column.png) iaas_user_id     | varchar(100)                   |
| ![](images/column.png) iaas_user_pw     | varchar(100)                   |
| ![](images/column.png) paas_user_id     | varchar(100)                   |
| ![](images/column.png) paas_user_pw     | varchar(100)                   |
| ![](images/column.png) caas_user_id     | varchar(100)                   |
| ![](images/column.png) caas_user_pw     | varchar(100)                   |
| ![](images/column.png) caas_user_use_yn | varchar(1)                     |
| ![](images/column.png) iaas_user_use_yn | varchar(1)                     |
| ![](images/column.png) paas_user_use_yn | varchar(1)                     |
| ![](images/column.png) updated_at       | datetime                       |
| ![](images/column.png) created_at       | datetime = current_timestamp() |

**![](images/table.png) vms**  
: PaaS-TA(AP) VM 정보를 관리한다.

| Column                                 | Properties                     |
|----------------------------------------|--------------------------------|
| ![](images/primary-column.png) id      | int unsigned (auto increment)  |
| ![](images/primary-column.png) zone_id | int                            |
| ![](images/column.png) name            | varchar(200)                   |
| ![](images/column.png) ip              | varchar(15)                    |
| ![](images/column.png) vm_type         | varchar(3)                     |
| ![](images/column.png) reg_date        | datetime = current_timestamp() |
| ![](images/column.png) reg_user        | varchar(36) = 'system'         |
| ![](images/column.png) modi_date       | datetime = current_timestamp() |
| ![](images/column.png) modi_user       | varchar(36) = 'system'         |

**![](images/table.png) zones**  
: PaaS-TA(AP) Zone 정보를 관리한다.

| Column                                 | Properties                     |
|----------------------------------------|--------------------------------|
| ![](images/primary-column.png) id      | int unsigned (auto increment)  |
| ![](images/column.png) name            | varchar(200)                   |
| ![](images/column.png) reg_date        | datetime = current_timestamp() |
| ![](images/column.png) reg_user        | varchar(36) = 'system'         |
| ![](images/column.png) modi_date       | datetime = current_timestamp() |
| ![](images/column.png) modi_user       | varchar(36) = 'system'         |


### [Index](https://github.com/PaaS-TA/Guide) > [User Guide](user_guide.md) > Monitoring MariaDB

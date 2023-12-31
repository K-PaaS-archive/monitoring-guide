### [Index](https://github.com/PaaS-TA/Guide) > [Monitoring Install](PAAS-TA_MONITORING_INSTALL_GUIDE.md) > Monitoring Dashboard


# Monitoring Dashboard Install Guide
1. [개요](#1)
2. [PaaS-TA Monitoring Dashboard 설치](#2)  
  2.1. [사전 설정 확인](#2.1)  
  2.2. [설치 파일 다운로드](#2.2)  
  2.3. [PaaS-TA Monitoring Dashboard 설치를 위한 설정](#2.3)  
  2.4. [PaaS-TA Monitoring Dashboard 설치](#2.4)
3. [PaaS-TA Monitoring Dashboard 접속](#3)  


## <div id="1">1. 개요
본 문서는 BOSH 기반 PaaS-TA(AP) 환경 모니터링을 위한 PaaS-TA Monitoring Dashboard 설치에 관한 내용을 다루고 있다.  
PaaS-TA Monitoring Dashboard 설치에는 다음 기능들이 포함된다.

1. PaaS-TA 환경의 시스템 자원 정보(Metric Data) 확인
2. PaaS-TA 환경의 시스템 자원 정보(Metric Data) 기반 알람 설정
3. PaaS-TA 환경의 로그 정보 조회

> ⚠️ **Monitoring Dashboard** v5.6.x 이하에서는 '3. PaaS-TA 환경의 로그 정보 조회'의 로깅 기능을 위해 Logsearch Deployment를 별도 설치하여야 했으나 v5.7.x 이후부터는 설치시 로깅 기능이 함께 포함된다. v5.6.x 이하 버전 사용 시에 Logsearch Deployment 설치는 [여기](PAAS-TA_MONITORING_LOGSEARCH_INSTALL.md)를 참고한다.


## <div id="2">2. PaaS-TA Monitoring Dashboard 설치


### <div id="2.1">2.1. 사전 설정 확인
1. BOSH 설치 및 BOSH 로그인이 되어 있어야 한다.
2. 'cloud-config'와 'runtime-config'가 업데이트 되어 있는지 확인한다.
3. Stemcell 목록을 확인하여 설치에 필요한 Stemcell이 업로드 되어 있는 것을 확인한다.
4. PaaS-TA(AP)가 설치되어 있어야 하며 BOSH와 PaaS-TA(AP)를 설치하는 과정에서 모니터링 옵션을 포함하여 설치해야 한다.
5. 만약 IaaS 환경에 대한 모니터링을 필요로 할 경우 반드시 Zabbix Package 설치가 선행 되어야 한다.

**│ cloud-config 확인**

```shell script
$ bosh -e {director-name} cloud-config
```

**│ runtime-config 확인**

```shell script
$ bosh -e {director-name} runtime-config
```

**│ Stemcell 확인**

```shell script
$ bosh -e {director-name} stemcells
```


### <div id="2.2">2.2. 설치 파일 다운로드
PaaS-TA Monitoring Dashbord를 설치하기 위한 Deployment를 내려 받는다. 만약 이미 설치 Deployment를 모두 내려 받은 상태라면 해당 단계는 건너뛸 수 있다.

```shell script
$ cd ~/workspace

$ git clone https://github.com/paas-ta/common.git
$ git clone https://github.com/PaaS-TA/paasta-deployment.git
$ git clone https://github.com/paas-ta/monitoring-deployment.git
```


### <div id="2.3">2.3. PaaS-TA Monitoring Dashboard 설치를 위한 설정
**│ common_vars.yml**

`common/common_vars.yml` 파일은 PaaS-TA 환경 및 각종 Deployment 설치시 필요한 공통 변수 설정을 담고 있다. 다음 파일 예제를 실제 환경 구성시에 참고하여 작성할 수 있다.

```yaml
# BOSH INFO
bosh_ip: "10.0.1.6"				# BOSH IP
bosh_url: "https://10.0.1.6"				# BOSH URL (e.g. "https://00.000.0.0")
bosh_client_admin_id: "admin"			# BOSH Client Admin ID
bosh_client_admin_secret: "ert7na4jpewscztsxz48"	# BOSH Client Admin Secret('echo $(bosh int ~/workspace/paasta-deployment/bosh/{iaas}/creds.yml --path /admin_password)' 명령어를 통해 확인 가능)
bosh_director_port: 25555			# BOSH director port
bosh_oauth_port: 8443				# BOSH oauth port
bosh_version: 271.2				# BOSH version('bosh env' 명령어를 통해 확인 가능, on-demand service용, e.g. "271.2")

# PAAS-TA INFO
system_domain: "61.252.53.246.nip.io"		# Domain (nip.io를 사용하는 경우 HAProxy Public IP와 동일)
paasta_admin_username: "admin"			# PaaS-TA Admin Username
paasta_admin_password: "admin"			# PaaS-TA Admin Password
paasta_nats_ip: "10.0.1.121"
paasta_nats_port: 4222
paasta_nats_user: "nats"
paasta_nats_password: "7EZB5ZkMLMqT73h2JtxPv1fvh3UsqO"	# PaaS-TA Nats Password (CredHub 로그인후 'credhub get -n /micro-bosh/paasta/nats_password' 명령어를 통해 확인 가능)
paasta_nats_private_networks_name: "default"	# PaaS-TA Nats 의 Network 이름
paasta_database_ips: "10.0.1.123"		# PaaS-TA Database IP (e.g. "10.0.1.123")
paasta_database_port: 5524			# PaaS-TA Database Port (e.g. 5524(postgresql)/13307(mysql)) -- Do Not Use "3306"&"13306" in mysql
paasta_database_type: "postgresql"                      # PaaS-TA Database Type (e.g. "postgresql" or "mysql")
paasta_database_driver_class: "org.postgresql.Driver"   # PaaS-TA Database driver-class (e.g. "org.postgresql.Driver" or "com.mysql.jdbc.Driver")
paasta_cc_db_id: "cloud_controller"		# CCDB ID (e.g. "cloud_controller")
paasta_cc_db_password: "cc_admin"		# CCDB Password (e.g. "c418e687c4Kx!" 영어/숫자/특수문자 혼용 8자리 이상)
paasta_uaa_db_id: "uaa"				# UAADB ID (e.g. "uaa")
paasta_uaa_db_password: "uaa_admin"		# UAADB Password (e.g. "ifb2497iEA5!" 영어/숫자/특수문자 혼용 8자리 이상)
paasta_api_version: "v3"

# UAAC INFO
uaa_client_admin_id: "admin"			# UAAC Admin Client Admin ID
uaa_client_admin_secret: "admin-secret"		# UAAC Admin Client에 접근하기 위한 Secret 변수
uaa_client_portal_secret: "clientsecret"	# UAAC Portal Client에 접근하기 위한 Secret 변수

# paasta-monitoring & pinpoint-monitoring deployment configuration
metric_url: "10.0.1.101"                  # influxdb IP
syslog_address: "10.0.1.100"              # td-agent IP
syslog_port: "2514"                       # td-agent Port
syslog_transport: "udp"                   # td-agent Logging Protocol
monitoring_api_url: "10.0.1.88"           # monitoring-web IP
saas_monitoring_url: "10.0.1.89"          # haproxy_webui IP
pinpoint_was_ip: "10.0.1.90"              # pinpoint_web IP

# zabbix-agent configuration (Essential setting when using IaaS monitoring option)
server_ip: "xxx.xxx.xxx.xxx"              # Zabbix server (or Proxy) IP address
listen_port: "10050"                      # Zabbix server (or Proxy) Port number
server_active: "xxx.xxx.xxx.xxx:10051"    # Zabbix server (or Proxy) IP:Port string
host_metadata: "paasta"                   # Metadata for Zabbix Agent autoregistration

### Portal INFO
portal_web_user_ip: "52.78.88.252"
portal_web_user_url: "http://portal-web-user.52.78.88.252.nip.io" 
portal_web_user_language: ["ko", "en"]             # portal webuser language list (e.g. ["ko", "en"])
portal_web_admin_language: ["ko", "en"]             # portal webadmin language list (e.g. ["ko", "en"])

### ETC INFO
abacus_url: "http://abacus.61.252.53.248.nip.io"	# abacus url (e.g. "http://abacus.xxx.xxx.xxx.xxx.nip.io")
```

**│ paasta-monitoring-vars.yml**  

`monitoring-deployment/paasta-monitoring/paasta-monitoring-vars.yml` 파일은 PaaS-TA Monitoring Dashboard 설치시 필요한 각종 변수 설정을 담고 있다. 내용 중 `mariadb` 및 `influxdb` 계정 등은 보안 설정 및 모듈 간 계정 정보가 연결된 부분이 있어 이를 변경하여 배포할 경우 관련 모듈이 정상적으로 동작하지 않을 수 있다. 따라서 이를 수정하여 사용하기 위해서는 [monitoring-dashboard-release](https://github.com/PaaS-TA/monitoring-dashboard-release) 또는 [monitoring-influxdb-release](https://github.com/PaaS-TA/monitoring-influxdb-release) 저장소에서 `job` 디렉토리 내의 관련 파일의 수정이 필요하다. 다음 파일 예제를 실제 환경 구성시에 참고하여 작성할 수 있다. monitoring web을 Private IP로 배포하려면 enable_private_network를 yes로 설정해야 한다.

```yaml
# SERVICE VARIABLE
inception_os_user_name: "ubuntu"
mariadb_ip: "10.200.1.102"            # MariaDB VM Private IP
mariadb_port: "7706"                  # PaaS-TA Database Port (e.g. 7706(mariadb)) -- Do Not Use "3306" in mysql
mariadb_username: "root"              # MariaDB Root 계정 Username
mariadb_password: "PaaS-TA2020"       # MariaDB Root 계정 Password. 영문/숫자/특수문자 혼용 8자 이상
director_name: "micro-bosh"           # BOSH Director 명
resource_url: "resource_url"          # TBD
paasta_deploy_name: "paasta"          # PaaS-TA Deployment 명
paasta_cell_prefix: "cell"            # PaaS-TA Cell 명
smtp_url: "smtp.naver.com"            # SMTP Server URL
smtp_port: "587"                      # SMTP Server Port
mail_sender: "aaa@naver.com"          # SMTP Server Admin ID
mail_password: "aaaa"                 # SMTP Server Admin Password
mail_enable: "true"                   # Alarm 발생시 Mail전송 여부
mail_tls_enable: "true"               # SMTP 서버 인증시 TLS모드인경우 true
redis_ip: "10.200.1.103"              # Redis Private IP
redis_password: "PaaS-TA2020"         # Redis 인증 Password. 영문/숫자/특수문자 혼용 8자 이상
redis_protected_mode: "yes"           # Redis 루프백 인터페이스 쿼리 응답 설정
influxdb_username: "admin"            # Influxdb Admin 계정 Username
influxdb_password: "PaaS-TA2020"      # Influxdb Admin 계정 Password
influxdb_interval: "30d"              # Influxdb Retention Policy (bootstrapper)
influxdb_https_enabled: "true"        # Influxdb HTTPS 설정
utc_time_gap: "9"                     # UTC Time Zone과 Client Time Zone과의 시간 차이
public_network_name: "vip"            # Monitoring-WEB Public Network Name
system_type: "PaaS,CaaS,SaaS,IaaS"    # 모니터링할 환경 선택
prometheus_ip: "52.78.16.121"         # Kubernates의 prometheus-prometheus-prometheus-oper-prometheus-0 Pod의 Node IP
kubernetes_ip: "52.78.16.121"         # Kubernates의 서비스 API IP
pinpoint_was_ip: "10.0.1.152"         # Pinpoint HAProxy WEBUI Private IP
cassbroker_ip: "3.36.38.199"          # CaaS 서비스 로그인 인증 처리를 위한 API IP (Kubernetes Master IP/service-common-api-deployment)
kubernetes_token: "eyJhbGciOiJSUzI1NiIsImtpZCI6IlMtbHpvLUYybGpiejl4c1ZqelRGRnFlX3pxaVFkS2NQOWhpWEJLS1JXckUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrOHNhZG1pbi10b2tlbi12cWhudiIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJrOHNhZG1pbiIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImExMGVkODgyLTU1ZGEtNGNmYS04Y2ZmLThiOTdiZTQzODE4MSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprdWJlLXN5c3RlbTprOHNhZG1pbiJ9.QZ3mTvdyaPwzDt7mtDoDYlaCxEqN7QIpWTIpUUCJm6qurOonhJd_kdmvhQsylkft6z-Pp4odMr6eQcTD3WwUQ95UMqvQirLZOjLF7MU07CBIxWvhIDK5qx3xrYEa5KswuhfTNre4py9I-tPV9_vHxRNcwZUjnBGo_BimuwJgqG_1LsZjXvdIeJfMQlEY2LokUDt07bMoUtH9sWLKHv8-rZfiMU1fGfifz9NwQ54Uh-CVspbg-YaJbVC6tnbyriuTNciViOth6Onwx_xuzBfFGRlh6ck0HlYKYz5-JxEpZy3zJwoNfukVmjl-4gNXb67Esm7rQyjHFMF2Z2c2EgDQEw"
enable_private_network: "yes"         # Monitoring 웹을 private IP로 배포하려면 yes로 설정
  
# Zabbix API INFO
zabbix_host: "http://10.200.1.200/zabbix/api_jsonrpc.php"
zabbix_admin_id: "Admin"
zabbix_admin_pw: "zabbix"

# Openstack INFO
openstack_region: "RegionOne"
openstack_domain: "default"
openstack_username: "xxxx"
openstack_password: "xxxx"
openstack_tenant_name: "paas-ta-monitoring"
openstack_tenant_id: "3f7134b979074ea493c265ca39cc1ead"
openstack_endpoint: "http://xxx.xxx.xxx.xxx:5000/v3"
openstack_keystone_url: "http://xxx.xxx.xxx.xxx:5000/v3"

# TD-AGENT(Fluentd) INFO
td-agent_ip: "10.200.2.130"
logging_db_name: "logging_db"
logging_measurement_name: "logging_measurement"
logging_time_precision: "s"                # hour(h), minutes(m), second(s), millisecond(ms), microsecond(u), nanosecond(ns)
influxdb_http_port: "8086"                 # default 8086

# STEMCELL
stemcell_os: "ubuntu-bionic"               # Stemcell OS
stemcell_version: "1.91"                   # Stemcell Version

# REDIS
redis_azs: ["z1"]                          # Redis 가용 존
redis_instances: 1                         # Redis 인스턴스 수
redis_vm_type: "small"                     # Redis VM 종류
redis_network: "default"                   # Redis 네트워크

# SANITY-TEST
sanity_tests_azs: ["z1"]                   # Sanity-Test 가용 존
sanity_tests_instances: 1                  # Sanity-Test 인스턴스 수
sanity_tests_vm_type: "small"              # Sanity-Test VM 종류
sanity_tests_network: "default"	           # Sanity-Test 네트워크

# INFLUXDB
influxdb_azs: ["z1"]                       # InfluxDB 가용 존
influxdb_instances: 1                      # InfluxDB 인스턴스 수
influxdb_vm_type: "large"                  # InfluxDB VM 종류
influxdb_network: "default"                # InfluxDB 네트워크
influxdb_persistent_disk_type: "10GB"      # InfluxDB 영구 Disk 종류

# MARIADB
mariadb_azs: ["z1"]                        # MariaDB 가용 존
mariadb_instances: 1                       # MariaDB 인스턴스 수
mariadb_vm_type: "medium"                  # MariaDB VM 종류
mariadb_network: "default"                 # MariaDB 네트워크
mariadb_persistent_disk_type: "5GB"        # MariaDB 영구 Disk 종류

# MONITORING-BATCH
monitoring_batch_azs: ["z1"]               # Monitoring-Batch 가용 존
monitoring_batch_instances: 1              # Monitoring-Batch 인스턴스 수
monitoring_batch_vm_type: "small"          # Monitoring-Batch VM 종류
monitoring_batch_network: "default"        # Monitoring-Batch 네트워크

# IAAS-MONITORING-BATCH
iaas_monitoring_batch_azs: ["z1"]          # IAAS-Monitoring-Batch 가용 존
iaas_monitoring_batch_instances: 1         # IAAS-Monitoring-Batch 인스턴스 수
iaas_monitoring_batch_vm_type: "small"     # IAAS-Monitoring-Batch VM 종류
iaas_monitoring_batch_network: "default"   # IAAS-Monitoring-Batch 네트워크

# CAAS-MONITORING-BATCH
caas_monitoring_batch_azs: ["z1"]          # CAAS-Monitoring-Batch 가용 존
caas_monitoring_batch_instances: 1         # CAAS-Monitoring-Batch 인스턴스 수
caas_monitoring_batch_vm_type: "small"     # CAAS-Monitoring-Batch VM 종류
caas_monitoring_batch_network: "default"   # CAAS-Monitoring-Batch 네트워크

# SAAS-MONITORING-BATCH
saas_monitoring_batch_azs: ["z1"]          # SAAS-Monitoring-Batch 가용 존
saas_monitoring_batch_instances: 1         # SAAS-Monitoring-Batch 인스턴스 수
saas_monitoring_batch_vm_type: "small"     # SAAS-Monitoring-Batch VM 종류
saas_monitoring_batch_network: "default"   # SAAS-Monitoring-Batch 네트워크

# MONITORING-WEB
monitoring_web_azs: ["z1"]                 # Monitoring-WEB 가용 존
monitoring_web_instances: 1                # Monitoring-WEB 인스턴스 수
monitoring_web_vm_type: "small"            # Monitoring-WEB VM 종류
monitoring_web_network: "default"          # Monitoring-WEB 네트워크

# TD-AGENT (Fluentd)
td-agent_azs: ["z1"]                       # Monitoring-WEB 가용 존
td-agent_instances: 1                      # Monitoring-WEB 인스턴스 수
td-agent_vm_type: "small"                  # Monitoring-WEB VM 종류
td-agent_network: "default"                # Monitoring-WEB 네트워크
```

**│ deploy-paasta-monitoring.sh**  

```shell script
#!/bin/bash

# paasta-monitoring-vars.yml 파일에서 IaaS 모니터링 옵션이 사용되는지 확인하고 조건에 따라 iaas-monitoring-batch VM 배포 및 zabbix-agent Addon 여부를 분기한다.
ScanIaaSOption=`grep IaaS paasta-monitoring-vars.yml`
enablePrivateNetworkOpt=`grep 'enable_private_network' paasta-monitoring-vars.yml`

if [ -n "$ScanIaaSOption" ]; then
    if [[ "$enablePrivateNetworkOpt" =~ yes ]]; then
	bosh -e micro-bosh -n -d paasta-monitoring deploy paasta-monitoring.yml \
          -o use-public-network-aws.yml \
	  -o use-private-monitoring-web.yml \
          -o addons/enable-zabbix-agent.yml \
          -l paasta-monitoring-vars.yml \
          -l ../../common/common_vars.yml
    else
        bosh -e micro-bosh -n -d paasta-monitoring deploy paasta-monitoring.yml \
          -o use-public-network-aws.yml \
          -o addons/enable-zabbix-agent.yml \
          -l paasta-monitoring-vars.yml \
          -l ../../common/common_vars.yml
    fi
else
    if [[ "$enablePrivateNetworkOpt" =~ yes ]]; then
	bosh -e micro-bosh -n -d paasta-monitoring deploy paasta-monitoring.yml \
          -o use-public-network-aws.yml \
	  -o use-private-monitoring-web.yml \
          -o addons/disable-iaas-monitoring-batch.yml \
          -l paasta-monitoring-vars.yml \
          -l ../../common/common_vars.yml
    else
	bosh -e micro-bosh -n -d paasta-monitoring deploy paasta-monitoring.yml \
          -o use-public-network-aws.yml \
          -o addons/disable-iaas-monitoring-batch.yml \
          -l paasta-monitoring-vars.yml \
          -l ../../common/common_vars.yml
    fi
fi
```

### <div id="2.4">2.4. PaaS-TA Monitoring Dashboard 설치
이전 단계를 통해서 PaaS-TA Monitoring Dashboard 설치를 위한 매니페스트 파일 및 변수 설정 파일의 구성이 완료되었다면 `deploy-paasta-monitoring.sh` 파일을 사용하여 설치를 시작할 수 있다.

```shell script
$ cd ~/workspace/monitoring-deployment/paasta-monitoring
$ source deploy-paasta-monitoring.sh
```

배포가 완료되었다면 다음 명령을 이용해 배포 상태를 확인할 수 있다.

```shell script
$ bosh vms
```

![](images/paasta-monitoring_v5.7.0.png)


## <div id="3">3. PaaS-TA Monitoring Dashboard 접속
웹 브라우저를 이용해 ***http://{monitoring-web_ip}:8080/public/login.html***에 접속하여 계정을 생성한 후 PaaS-TA Monitoring Dashboard를 이용할 수 있다. Login 화면에서 **Register now!** 버튼을 클릭한다.

![](images/monit_login_5.0.png)

PaaS Certification 항목에는 PaaS-TA(AP) 배포시 공통 변수 파일(`common_vars.yml`)에서 설정한 계정 정보를 입력한다. IaaS Certification 항목에는 모니터링 배포시에 필요한 변수 파일(`paasta-monitoring-vars.yml`)에 설정한 계정 정보를 입력한다. Member Info 항목에는 사용자가 사용할 아이디와 비밀번호를 입력한다. 각 항목 별로 **인증하기** 버튼을 클릭하여 인증 확인을 거쳐야 하며 최종적으로 **Join** 버튼을 클릭하면 계정 생성이 완료된다. 

![](images/member_join_5.0.png)

생성한 계정 정보를 이용하여 로그인에 성공하면 다음과 같은 대시보드 메인 화면을 확인할 수 있다. 여기까지 확인했다면 PaaS-TA Monitoring Dashboard 설치에 성공한 것이다.

![](images/monit_main_5.0.png)


### [Index](https://github.com/PaaS-TA/Guide) > [Monitoring Install](PAAS-TA_MONITORING_INSTALL_GUIDE.md) > Monitoring Dashboard

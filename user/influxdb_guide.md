### [Index](https://github.com/PaaS-TA/Guide) > [User Guide](user_guide.md) > Monitoring InfluxDB


# Monitoring InfluxDB User Guide
1. [개요](#1)
2. [Monitoring InfluxDB 메저먼트/컬럼 명세](#2)


## <div id="1">1. 개요
이 문서는 PaaS-TA Monitoring Dashboard 배포시 생성되는 influxdb VM 내 설치된 InfluxDB의 데이터베이스와 메저먼트/컬럼 구조에 대한 명세와 가이드를 제공하기 위해 작성되었다.


## <div id="2">2. Monitoring InfluxDB 메저먼트/컬럼 명세
### 2.1. bosh_metric_db
**![](images/table.png) bosh_metrics**  
: BOSH의 메트릭 정보를 저장한다.

| Column                            | Description                   |
|-----------------------------------|-------------------------------|
| ![](images/column.png) time       | Time                          |
| ![](images/column.png) deployment | Deployment Name               |
| ![](images/column.png) id         | BOSH ID                       |
| ![](images/column.png) index      | -                             |
| ![](images/column.png) metricname | Metric Info (CPU/Memory/Disk) |
| ![](images/column.png) value      | Metric Value                  |

**![](images/table.png) bosh_process_metrics**  
: BOSH의 프로세스 메트릭 정보를 저장한다.

| Column                            | Description          |
|-----------------------------------|----------------------|
| ![](images/column.png) time       | Time                 |
| ![](images/column.png) deployment | Deployment Name      |
| ![](images/column.png) id         | BOSH ID              |
| ![](images/column.png) index      | -                    |
| ![](images/column.png) mem_usage  | Process Memory Usage |
| ![](images/column.png) metricname | -                    |
| ![](images/column.png) proc_index | Process Index        |
| ![](images/column.png) proc_name  | Process Name         |
| ![](images/column.png) proc_pid   | Process PID          |
| ![](images/column.png) proc_ppid  | Process PPID         |
| ![](images/column.png) start_time | Process Start Time   |


### 2.2. cf_metric_db
**![](images/table.png) cf_metrics**  
: PaaS-TA(CF)의 Instance(VM)의 메트릭 정보를 저장한다.

| Column                            | Description                   |
|-----------------------------------|-------------------------------|
| ![](images/column.png) time       | Time                          |
| ![](images/column.png) deployment | Deployment Name               |
| ![](images/column.png) id         | Instance ID                   |
| ![](images/column.png) index      | -                             |
| ![](images/column.png) ip         | Instance IP                   |
| ![](images/column.png) metricname | Metric Info (CPU/Memory/Disk) |
| ![](images/column.png) origin     | Instance Name                 |
| ![](images/column.png) value      | Metric Value                  |

**![](images/table.png) cf_process_metrics**  
: PaaS-TA(CF)의 Instance(VM)의 프로세스 메트릭 정보를 저장한다.

| Column                            | Description          |
|-----------------------------------|----------------------|
| ![](images/column.png) time       | Time                 |
| ![](images/column.png) deployment | Deployment Name      |
| ![](images/column.png) id         | Instance ID          |
| ![](images/column.png) index      | -                    |
| ![](images/column.png) ip         | Instance IP          |
| ![](images/column.png) mem_usage  | Process Memory Usage |
| ![](images/column.png) metricname | -                    |
| ![](images/column.png) origin     | Instance Name        |
| ![](images/column.png) proc_index | Process Index        |
| ![](images/column.png) proc_name  | Process Name         |
| ![](images/column.png) proc_pid   | Process PID          |
| ![](images/column.png) proc_ppid  | Process PPID         |
| ![](images/column.png) start_time | Process Start Time   |


### 2.3. container_metric_db
**![](images/table.png) container_metrics**  
: PaaS-TA(CF) 환경에 배포된 Container(App) 메트릭 정보를 저장한다.

| Column                                     | Description                   |
|--------------------------------------------|-------------------------------|
| ![](images/column.png) time                | Time                          |
| ![](images/column.png) cell_ip             | diego-cell VM IP              |
| ![](images/column.png) container_id        | Container ID                  |
| ![](images/column.png) container_interface | Container Interface           |
| ![](images/column.png) device              | Mounted Route Info            |
| ![](images/column.png) machine             | diego-cell VM ID              |
| ![](images/column.png) name                | Metric Info (CPU/Memory/Disk) |
| ![](images/column.png) type                | Metric Type (Limit/Usage)     |
| ![](images/column.png) value               | Metric Value                  |

### 2.4. logging_db
**![](images/table.png) logging_measurement**  
: PaaS-TA(CF)의 Instance(VM)의 로그 정보를 저장한다.

| Column                           | Description        |
|----------------------------------|--------------------|
| ![](images/column.png) time      | Time               |
| ![](images/column.png) _seq      | -                  |
| ![](images/column.png) extradata | Extra Data         |
| ![](images/column.png) host      | Instance Host Info |
| ![](images/column.png) ident     | Log Identity       |
| ![](images/column.png) message   | Log Message        |
| ![](images/column.png) msgid     | -                  |
| ![](images/column.png) pid       | -                  |


### [Index](https://github.com/PaaS-TA/Guide) > [User Guide](user_guide.md) > Monitoring InfluxDB

### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > [Monitoring Architecture](PAAS-TA_MONITORING_ARCHITECTURE.md) > IaaS


# IaaS Monitoring Architecture


### │ IaaS  Monitoring Architecture
IaaS 서비스 모니터링 운영환경은 IaaS는 Openstack과 Monasca를 기반으로 구성되어 있다.  
IaaS는 Openstack Node에 monasca Agent가 설치되어 Metric Data를 Monasca에 전송하여 InfluxDB에 저장한다.  
PaaS는 PaaS-TA에 모니터링 Agent가 설치되어 InfluxDB에 전송 저장한다.  
Log Agent도 IaaS/PaaS에 설치되어 Log Data를 각각의 Log Repository에 전송한다.

![IaaSTa_Monit_architecure_Image]


### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > [Monitoring Architecture](PAAS-TA_MONITORING_ARCHITECTURE.md) > IaaS


<!-- Images Links -->
[IaaSTa_Monit_architecure_Image]:./images/iaas-archi.png
### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > Monitoring Install


# PaaS-TA Monitoring Install Guide


### │ PaaS-TA Monitoring Install Process
본 가이드에서는 하기에 나열된 가이드의 순서대로 설치를 진행할 것을 권장하고 있으며, 가이드 중 📑 아이콘으로 표시된 가이드는 <b>PaaS-TA 플랫폼</b>에서 최소한의 모니터링 기능을 사용하기 위한 필수 설치 가이드를 의미한다. IaaS 모니터링을 사용한다면 ① + ② 항목 모두를 순서대로 설치하고, IaaS 모니터링을 사용하지 않는다면 ② 항목부터 순서대로 설치한다.

 ① IaaS 모니터링을 사용할 경우,  
　📄 [[IaaS] Infrastructure Monitoring - Zabbix Package 설치](#)  
　　▸ [Zabbix Server 설치](PAAS-TA_MONITORING_ZABBIX-SERVER_INSTALL.md)  
　　▸ [Zabbix Proxy 설치](PAAS-TA_MONITORING_ZABBIX-PROXY_INSTALL.md)  
　　▸ [Zabbix Agent 설치](PAAS-TA_MONITORING_ZABBIX-AGENT_INSTALL.md)  

 ② IaaS 모니터링을 사용하지 않을 경우,  
　📑 **[BOSH (+Monitoring Dashboard) 설치](PAAS-TA_BOSH2_MONITORING_INSTALL_GUIDE.md)**  
　📑 **[PaaS-TA (+Monitoring Dashboard) 설치](PAAS-TA_CORE_MONITORING_INSTALL_GUIDE.md)**  
　📑 **[Monitoring Dashboard 설치](PAAS-TA_MONITORING_PAAS-TA_MONITORING_INSTALL.md)**  
　📄 [[PaaS] Log Monitoring - Logsearch 설치](PAAS-TA_MONITORING_LOGSEARCH_INSTALL.md)  
　📄 [[SaaS] Application Monitoring - Pinpoint Monitoring 설치](PAAS-TA_MONITORING_PINPOINT_MONITORING_INSTALL.md)  
　　▸ [Pinpoint Java Buildpack 생성/등록](PAAS-TA_MONITORING_CREATE_PINPOINT_JAVA_BUILDPACK.md)  
　　▸ [Sample Application & Pinpoint Service 바인딩/푸시](PAAS-TA_MONITORING_PUSH_SAMPLE_APPLICATION.md)      
　📄 [[CaaS] Container Monitoring - Prometheus 설치](PAAS-TA_MONITORING_CONTAINER_SERVICE_INSTALL.md)  

<table>
  <tr>
    <td>⚠️ <b>PaaS-TA 플랫폼</b>에서 모니터링 기능(대시보드)을 사용할 경우 반드시 <b>BOSH</b>와 <b>PaaS-TA</b> 배포 시에 모니터링에 필요한 옵션을 사용한 배포 작업이 필수 선행되어야 한다(#1, #2 설치 가이드 참고).<br>
        ⚠️ Zabbix Package 설치는 IaaS 모니터링 기능을 사용할 경우 반드시 설치되어야 하며 가장 먼저 설치할 것을 권장하고 있다.</tr>
</table>


### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > Monitoring Install

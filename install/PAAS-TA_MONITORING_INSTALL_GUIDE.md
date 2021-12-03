### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > Monitoring Install


# PaaS-TA Monitoring Install Guide


### │ PaaS-TA Monitoring Install Process
본 가이드에서는 PaaS-TA 플랫폼에서 모니터링 기능을 사용하기 위해 하기에 나열된 가이드의 순서대로 설치를 진행할 것을 권장하고 있다. 따라서 IaaS 모니터링 옵션을 사용한다면 **① + ② 항목을 순서대로 설치**하고, IaaS 모니터링 옵션을 사용하지 않는다면 **② 항목부터 순서대로 설치**한다.

가이드 중 📑 아이콘으로 별도 표시된 가이드는 최소한의 모니터링 기능을 사용하기 위해서 필수로 설치해야 하는 가이드를 의미하며 그 외 모니터링 설치 가이드는 사용자의 의사에 따라 선택적(Optional)으로 설치할 수 있다. 따라서 📑 가이드만 설치하는 것은 PaaS-TA 플랫폼에서 지원하는 여러 모니터링 옵션 중 최소한의 모니터링 기능(PaaS 모니터링)만을 사용하는 최소 옵션이자 필수 옵션(모니터링 기능을 사용할 때)을 의미한다.

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
    <td>⚠️ Zabbix Package 설치는 IaaS 모니터링 기능을 사용할 경우에 반드시 설치되어야 하며 가장 먼저 설치할 것을 권장하고 있다.<br>
    ⚠️ <b>PaaS-TA 플랫폼</b>에서 모니터링 기능(Monitoring Dashboard)을 사용할 경우 반드시 <b>BOSH</b>와 <b>PaaS-TA</b> 설치 시에 모니터링에 필요한 옵션을 사용한 설치 작업이 필수 선행되어야 한다.</td>        
  </tr>
</table>


### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > Monitoring Install

### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > Monitoring Install


# PaaS-TA Monitoring Install Guide


### │ PaaS-TA Monitoring Install Process


#### ⛤ ─ *Essential Installation.*  
　 [[IaaS] Infrastructure Monitoring - Zabbix 설치](#) : IaaS 모니터링을 이용할 경우에만 설치  
 　　▸ [Zabbix Server 설치](PAAS-TA_MONITORING_ZABBIX-SERVER_INSTALL.md)  
 　　▸ [Zabbix Proxy 설치](PAAS-TA_MONITORING_ZABBIX-PROXY_INSTALL.md)  
 　　▸ [Zabbix Agent 설치](PAAS-TA_MONITORING_ZABBIX-AGENT_INSTALL.md)  
⛤ 1. [BOSH (+Monitoring Dashboard) 설치](PAAS-TA_BOSH2_MONITORING_INSTALL_GUIDE.md)  
⛤ 2. [PaaS-TA (+Monitoring Dashboard) 설치](PAAS-TA_CORE_MONITORING_INSTALL_GUIDE.md)  
　 3. [[PaaS] Log Monitoring - Logsearch 설치](PAAS-TA_MONITORING_LOGSEARCH_INSTALL.md)  
　 4. [[SaaS] Application Monitoring - Pinpoint Monitoring 설치](PAAS-TA_MONITORING_PINPOINT_MONITORING_INSTALL.md)  
　 5. [[CaaS] Container Monitoring - Prometheus 설치](PAAS-TA_MONITORING_CONTAINER_SERVICE_INSTALL.md)  
⛤ 7. [**Monitoring Dashboard** 설치](PAAS-TA_MONITORING_PAAS-TA_MONITORING_INSTALL.md)

- Zabbix 설치는 IaaS 모니터링 기능을 활성화할 경우 반드시 설치되어야 하며, 가장 먼저 설치하는 것을 권장하고 있다.
- Zabbix Agent는 배포과정에서 자동으로 설치되므로 [Zabbix Agent 설치](PAAS-TA_MONITORING_ZABBIX-AGENT_INSTALL.md)  메뉴얼은 수동 설치시에만 참고한다.

<table>
  <tr>
    <td>⚠️ <b>PaaS-TA 플랫폼</b>에서 모니터링 기능(대시보드)을 사용할 경우, 반드시 <b>BOSH</b>와 <b>PaaS-TA</b> 배포 시에 모니터링에 필요한 옵션을 사용한 배포 작업이 필수 선행되어야 한다(#1, #2 설치 가이드 참고).</td>
  </tr>
</table>


### [Index](https://github.com/PaaS-TA/Guide/tree/working-new-template) > Monitoring Install
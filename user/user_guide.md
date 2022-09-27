### [Index](https://github.com/PaaS-TA/Guide) > User Guide


# PaaS-TA Monitoring User Guide


### │ Purpose
본 문서는 PaaS-TA 모니터링 플랫폼을 구성하는 컴포넌트 및 모듈에 대한 사용자 가이드를 제공하기 위해 작성되었다.


### │ Instance Group Composition
<table>
  <tr>
    <td><b>Instance</b></td>
    <td><b>Role</b></td>
  </tr>
  <tr>
    <td><b>mariadb</b></td>
    <td>PaaS-TA 플랫폼의 인스턴스 목록, 알람, 멤버 등의 정보를 담기 위한 관계형 데이터베이스가 동작</td>
  </tr>
  <tr>
    <td><b>influxdb</b></td>
    <td>PaaS-TA 플랫폼에서 모니터링된 메트릭 정보와 로그 정보를 담기 위한 시계열 데이터베이스가 동작</td>
  </tr>
  <tr>
    <td><b>redis</b></td>
    <td>사용자 인증, 세션 관리를 목적으로 하는 Key-Value 구조 등의 비정형 정보를 담기 위한 데이터베이스가 동작</td>
  </tr>
  <tr>
    <td><b>monitoring-batch</b></td>
    <td>PaaS 파트 알람을 위한 배치 모듈 동작</td>
  </tr>
  <tr>
    <td><b>caas-monitoring-batch</b></td>
    <td>CaaS 파트 알람을 위한 배치 모듈 동작</td>
  </tr>
  <tr>
    <td><b>saas-monitoring-batch</b></td>
    <td>SaaS 파트 알람을 위한 배치 모듈 동작</td>
  </tr>
  <tr>
    <td><b>iaas-monitoring-batch</b></td>
    <td>IaaS 파트 알람을 위한 배치 모듈 동작</td>
  </tr>
  <tr>
    <td><b>monitoring-web</b></td>
    <td>PaaS-TA 모니터링 플랫폼에서 지원하는 모니터링 관련 기능 및 각종 정보와 수치를 시각화한 웹 브라우저 기반 화면 제공</td>
  </tr>
  <tr>
    <td><b>monitoring-api</b></td>
    <td>PaaS-TA 모니터링 플랫폼에서 지원하는 모니터링 관련 기능을 통합 제공하는 API 모듈 및 Swagger 기반으로 작성된 API 가이드 제공</td>
  </tr>
  <tr>
    <td><b>td-agent</b></td>
    <td>PaaS-TA 플랫폼의 인스턴스에서 발생하는 로그를 수집하고 데이터베이스로 중계하는 로그 수집기(fluentd) 동작</td>
  </tr>
</table>


### │ User Guide Shortcut
- 📘 [Monitoring MariaDB User Guide (제작중)]()
- 📘 [Monitoring InfluxDB User Guide (제작중)]()
- 📘 [Monitoring Monitoring Web User Guide (제작중)]()
- 📘 [Monitoring API User Guide](monitoring-api_guide.md)


### [Index](https://github.com/PaaS-TA/Guide) > User Guide

---
title : JBoss EAP 7 무엇이며, 상용버전(JBoss)과 커뮤니티 버전(Wildfly)의 차이점
date : 2023-02-14 17:30:00 + 0900
categories : [WEB/WAS, JBOSS]
tags : [web, was, jboss, eap, eap 7.0, wildfly, open source]
render_with_liquid: false
---

# JBoss EAP(Enterprise Application Platform) 란 무엇인가 ? 

+ JBoss EAP 7는 개방형 표준을 기반으로 개발된 오픈소스 미들웨어 플랫폼으로 Java EE 7 인증을 받은 제품
+ Enterprise(기업) 환경에서 미들웨어가 갖추어야 하는 대용량 트랜잭션, 클러스터링(고가용성), 메시징, 분산 캐싱, 고성능 보장 등의 기술들을 제공
+ JBoss는 오픈소스 소프트웨어 개발 커뮤니티인 jboss.org 에서 개발 및 운영되고 있으며, 현재는 상용(Redhat) 플랫폼은 JBoss, 커뮤니티 플랫폼은 wildfly 라는 이름으로 변경됨. 
+ JBoss는 자바를 기반으로 하는 오픈소스 미들웨어의 브랜드명으로 JBoss 브랜드 안에는 JBoss Datagrid, JBoss Fuse 등 많은 미들웨어 제품들이 있다.
+ JBOSS EAP7 은 wildfly 10을 통합하여 제공됨.(JBoss RPM 설치 시 default 설치 경로가 `/opt/rh/eap7/root/usr/share/wildfly/` 이다.)


## JBoss EAP와 Wildfly의 차이점
+ JBoss는 Wildfly와 소스코드는 거의 동일하나 QA, 안정성, 성능 등을 개선한 기업용 오픈소스 서버
+ JBoss는 유료 Subscription을 구매 시 문제 발생 시 지원을 받을 수 있는 반면, Wildfly는 사용자 및 고객 스스로 문제를 해결해야한다.  

<br>

 __[Table 1] 상용버전(JBoss)과 커뮤니티 버전(Wildfly)의 차이점__

|            | Wildfly 10         | JBoss EAP 7 |
|:-----------|:-----------------|:---------------------------|
| Web URL    | widfly.org       | redhat.com or jboss.com    |
| 라이선스 비용 | 없음               | 없음                       |
| 기술지원	| 사용자 스스로 해결    | 제조사 기술지원(redhat)       |
| 소스코드 접근 | 완전한 접근 가능     | 완전한 접근 가능               |
| 대상        | 누구나             | 레드햇 서브스크립션 고객         |
| 개발        | 오픈소스 프로젝트 커뮤니티 | 오픈소스 프로젝트 커뮤니티 및 JBoss EAP 제품화 팀 | 
| 개선 및 향상  | 커뮤니티의 요구에 따른 임시 또는 실험적인 소프트웨어 변경   | 주요 릴리스, 소규모 릴리스, 패치 및 마이그레이션 도구를 포함한 구조화된 릴리스 과정 |
| 매뉴얼       | 프로젝트 컴포넌트에따라 다양                          | 전문적인 소프트웨어 설명서 |
| 품질        | 기능 검증을 위한 테스팅 위주                          | 매우 다양한 테스트 등이 통합된 우수한 품질 |
															 

## <b> Referances </b>
+ **OpenMaru**, <https://jboss6.openmaru.io/docs/01.JBoss_Introduction.html>
+ **Redhat Portal**, <https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/>






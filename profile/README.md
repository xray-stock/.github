# 📈 xray-stock

> 실시간 주식 시스템을 함께 고민하는 개발자 스터디

---

## 🙋‍♂️ About Us

**xray-stock**은 실시간 주식 데이터 처리 시스템을 직접 구현하고 분석해보는 개발자 중심의 스터디입니다.  
실제 주식 시장의 아키텍처, 데이터 흐름, 성능 문제, 거래의 신뢰성 등을 고민하며 **어떻게 돌아가는가?**에서 출발해  
**직접 만들어보자**를 목표로 합니다.

우리가 만드는 시스템이 실제 증권사만큼 완벽하지는 않더라도,  
**해피 해킹 정신으로 끝까지 부딪혀보는** 것에 의미를 둡니다.

---

## 🏗 시스템 아키텍처

```mermaid
graph LR
    A[📦 stock-generator<br/>시세 시뮬레이터] -->|현재: REST API<br/>향후: Kafka 등| B[⚙️ stock-service<br/>시세 처리 / 체결 서버]
    B -->|WebSocket<br/>실시간 체결 전파| C[🖥️ Web Viewer]
    C -->|REST API<br/>초기 종목/체결 조회| B
````

### 구성 요약

* **📦 stock-generator**
  @slicequeue이 구현. 가상의 주식 데이터를 생성

  * 현재는 stock-service로 **REST API 호출 방식의 라운드 로빈 전달**
  * 추후 Kafka 또는 Redis Stream 기반 **Producer → Consumer 구조**로 전환 예정

* **⚙️ stock-service**
  @slicequeue이 구현.

  * 시세 수신 및 체결 처리
  * Redis Pub/Sub 또는 Kafka 기반 수신 준비
  * 체결 결과를 WebSocket으로 Web Viewer에 브로드캐스트
  * 종목/체결 초기 정보는 REST API로 제공

* **🖥️ Web Viewer (예정)**

  * 실시간 체결 정보: **WebSocket 구독**
  * 초기 종목 목록/체결 히스토리: **REST API 호출**

> 이처럼 실시간성과 초기 정합성을 동시에 고려하여,
> **Socket + REST Hybrid 구조**로 Viewer 통신을 구성합니다.

---

## 🧩 Repository 구성

| 담당자           | 리포지토리                                                                      | 설명                                                                    |
| ------------- | -------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `@slicequeue` | [`stock-generator`](https://github.com/xray-stock/xray-stock-generator-sq) | `@slicequeue`이 구현한 **시세 발생기**. Redis에 랜덤 주식 데이터를 퍼블리시합니다.             |
| `@slicequeue` | [`stock-service`](https://github.com/xray-stock/xray-stock-service-sq)     | `@slicequeue`이 구현한 **주식 서비스 서버**. 시세 수신, 종목 관리, 체결 처리 및 실시간 브로드캐스트 담당 |
| `@choru90`    | [`choru-stock-mock`](https://github.com/xray-stock/choru-stock-mock)       | `@choru90`이 구현한 **체결 흐름 실험 서버**. 메시지 처리 로직과 흐름을 테스트하는 실습용 환경          |

---

## 💡 Why 'xray'?

엑스레이는 **보이지 않는 것을 투시**해 보여줍니다.
`xray-stock` 스터디도 겉으로 보이지 않는 시스템의 내부를 깊이 파고들어, **기술의 본질을 꿰뚫는 시선**을 지향합니다.

---

## 🔍 Topics We Explore

* Event-driven architecture
* Redis Pub/Sub & Kafka
* Spring Boot + MongoDB + RDB 혼합 설계
* 실시간 socket 인증과 통신 구조
* 주식 시장의 서킷 브레이커, 상·하한가 시스템
* 개발 생산성 향상 및 테스트 전략

---

## 📊 실시간 시스템 참고 자료 정리

* 🎥 [토스ㅣSLASH 22 - 애플 한 주가 고객에게 전달되기까지](https://www.youtube.com/watch?v=46QkQJGMv4I)
  *주식 매매 체결 처리, 대기열, 정합성 보장, 메시지 큐 사용 등 실제 증권 시스템에서의 고민과 구조 공유*

* 🎥 [토스ㅣSLASH 22 - 토스증권 실시간 시세 적용기](https://www.youtube.com/watch?v=tldwm64CUTo)
  *Kafka, 웹소켓 기반의 실시간 시세 전달, 성능 튜닝 및 시스템 아키텍처 소개*

---

## ⏰ 스터디 운영 방식

* 각자의 리포지토리에서 기능을 개발하고, 메인 레포로 PR을 보내며 코드 리뷰를 주말 일요일 아침 7시 30분 게더타운을 이용하여 서로 피드백합니다
* 서로의 구조, 방식, 개선 아이디어를 나누며 실제 서비스를 만드는 과정을 즐깁니다

---

## 👥 참여자

* [`@slicequeue`](https://github.com/slicequeue)
* [`@choru90`](https://github.com/choru90)

---

## 🍿 Fun Fact

* 첫 종목은 무려 **삼성전자**, 지금은 미국 **테슬라** 진행 중...
* 매주 일요일 아침, 졸린 눈 비비며 조기 축구가 아닌 **조기 코딩**에 뛰어드는 코딩 모임입니다 ⚽⚽🧑‍💻🧑‍💻
* 이따금씩 **"이거 실서비스에서도 이렇게 될까?"** 같은 깊은 토론이 벌어지기도 합니다

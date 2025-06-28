# 📈 xray-stock

> 실시간 주식 시스템을 기술적 구현을 함께 고민하는 개발자 스터디

---

## 🙋‍♂️ About Us

**xray-stock**은 실시간 주식 데이터 처리 시스템을 직접 구현하고 분석해보는 개발자 중심의 스터디입니다.  
실제 주식 시장의 아키텍처, 데이터 흐름, 성능 문제, 거래의 신뢰성 등을 고민하며 **"어떻게 돌아가는가?"**에서 출발해  
**"직접 만들어보자"**를 목표로 합니다.

우리가 만드는 시스템이 실제 증권사만큼 완벽하지는 않더라도,  
**해피 해킹 정신으로 끝까지 부딪혀보는** 것에 의미를 둡니다.

---

## 🏗 시스템 아키텍처

`xray-stock`은 다음과 같은 구조로 구성됩니다:

```

\[ 시세 발생기 ]
|
v
\[ 주식 서비스 서버 ]
|
v
\[ 뷰어 웹 페이지 ]

```

- **stock-generator**: 가상의 주식 데이터를 시뮬레이션하고 Redis Pub/Sub을 통해 퍼블리시합니다.
- **stock-service**: Redis로부터 시세를 수신하고, 종목 관리/체결/브로드캐스팅/DB저장 등의 핵심 로직을 담당합니다.
- **(예정) 웹 뷰어**: 실시간 시세 및 체결 정보를 소켓을 통해 보여주는 시각화 페이지입니다.

우리는 단순한 코드 작성이 아닌, **실제 시스템이 갖춰야 할 설계 요소들** — 이벤트 흐름, 메시지 정합성, 트래픽 대응 등을 고민하며 구조를 함께 다듬어가고 있습니다.

---

## 🧩 Repository 구성

| Repository | 설명 |
|------------|------|
| [`stock-generator`](https://github.com/xray-stock/xray-stock-generator-sq) | 가상의 시세 데이터를 시뮬레이션하고 Redis에 퍼블리시하는 서비스 |
| [`stock-service`](https://github.com/xray-stock/xray-stock-service-sq) | 실시간 시세, 종목 관리, 체결 이벤트 등을 처리하는 핵심 백엔드 서비스 |
| [`choru-stock-mock`](https://github.com/xray-stock/choru-stock-mock) | 체결 흐름과 메시지 처리 구조를 실험해보는 개인 실습 리포지토리 |
| (예정) `stock-client` | 실시간 소켓 기반의 체결 확인 및 차트 UI 구성 |

---

## 💡 Why 'xray'?

엑스레이는 **보이지 않는 것을 투시**해 보여줍니다.  
`xray-stock` 스터디도 겉으로 보이지 않는 시스템의 내부를 깊이 파고들어, **기술의 본질을 꿰뚫는 시선**을 지향합니다.

---

## 🔍 Topics We Explore

- Event-driven architecture
- Redis Pub/Sub & Kafka
- Spring Boot + MongoDB + RDB 혼합 설계
- 실시간 socket 인증과 통신 구조
- 주식 시장의 서킷 브레이커, 상·하한가 시스템
- 개발 생산성 향상 및 테스트 전략

---

## 📊 실시간 시스템 참고 자료 정리

- 🎥 [토스ㅣSLASH 22 - 애플 한 주가 고객에게 전달되기까지](https://www.youtube.com/watch?v=46QkQJGMv4I)  
  *주식 매매 체결 처리, 대기열, 정합성 보장, 메시지 큐 사용 등 실제 증권 시스템에서의 고민과 구조 공유*

- 🎥 [토스ㅣSLASH 22 - 토스증권 실시간 시세 적용기](https://www.youtube.com/watch?v=tldwm64CUTo)  
  *Kafka, 웹소켓 기반의 실시간 시세 전달, 성능 튜닝 및 시스템 아키텍처 소개*

---

## ⏰ 스터디 운영 방식

- **일요일 아침 조기 코딩**을 기본으로 합니다 ☀️
- 각자의 리포지토리에서 기능을 개발하고, 메인 레포로 PR을 보내며 코드 리뷰를 중심으로 피드백합니다
- 서로의 구조, 방식, 개선 아이디어를 나누며 실제 서비스를 만드는 과정을 즐깁니다

---

## 👥 참여자

| GitHub | 담당 리포지토리 |
|--------|-----------------|
| [`@slicequeue`](https://github.com/orgs/xray-stock/people/slicequeue) | [`stock-service`](https://github.com/xray-stock/xray-stock-service-sq), [`stock-generator`](https://github.com/xray-stock/xray-stock-generator-sq) |
| [`@choru90`](https://github.com/orgs/xray-stock/people/choru90) | [`choru-stock-mock`](https://github.com/xray-stock/choru-stock-mock) |

---

## 🍿 Fun Fact

- 첫 종목은 무려 **삼성전자**, 지금은 미국 **테슬라** 진행 중...  
- 매주 일요일 아침, 졸린 눈 비비며 조기 축구가 아닌 **조기 코딩**에 뛰어드는 코딩 모임입니다 ⚽⚽🧑‍💻🧑‍💻
- 이따금씩 **"이거 실서비스에서도 이렇게 될까?"** 같은 깊은 토론이 벌어지기도 합니다

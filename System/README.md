# [대규모 시스템 설계 기초]
- 1장. 사용자 수에 따른 규모 확장성: https://newwisdom.tistory.com/114
- 2장. 개략적인 규모 추정: https://newwisdom.tistory.com/115
- 3장. 시스템 설계 면접 공략법: https://newwisdom.tistory.com/116
- 4장. 처리율 제한 장치의 설계: https://newwisdom.tistory.com/117
- 5장. 안정 해시 설계: https://newwisdom.tistory.com/118
- 6장. 키-값 저장소 설계: https://newwisdom.tistory.com/120

# 시스템 확장을 위한 기법
- 웹 계층은 무상태 계층으로
- 모든 계층에 다중화 도입
- 가능한 한 많은 데이터를 캐시할 것
- 여러 데이터 센터를 지원할 것
- 정적 콘텐츠는 CDN을 통해 서비스 할것
- 데이터 계층은 샤딩을 통해 그 규모를 확장할 것
- 각 계층은 독립적 서비스로 분할할것
- 시스템을 지속적으로 모니터링하고, 자동화 도구들을 활용할 것

# 개략적인 규모추정 예
## 가정
- 월간 능동 사용자(monthly active user)는 3억(300million) 명이다.
- 50%의 사용자가 트위터를 매일 사용한다.
- 평균적으로 각 사용자는 매일 2건의 트윗을 올린다.
- 미디어를 포함하는 트윗은 10% 정도다.
- 데이터는 5년간 보관된다.

## 추정
### QPS(Query Per Second) 추정지
- 일간 능동 사용자(Daily Active User, DAU) = 3억 x 50% = 1.5억(150million)
- QPS = 1.5억 x 2트윗 / 24시간 / 60분 / 60초 = 약 3,500
- 최대 QPS(Peek QPS) = 2 x QPS = 약7,000
  
### 미디어 저장을 위한 저장소 요구량
- 평균 트윗 크기
  - tweet_id에 64바이트
  - 텍스트에 140바이트
  - 미디어에 1MB
- 미디어 저장소 요구량: 1.5억 x 2 x 10% x 1MB = 30TB/일
- 5년간 미디어를 보관하기 위한 저장소 요구량: 30TB x 365 x 5 = 약55PB

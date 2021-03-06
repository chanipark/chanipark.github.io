---
layout: post
title: '[TXGX] 클레이튼 넥스트'
subtitle: '[TXGX] 클레이튼 넥스트'
categories: review
tags: event
---

## 메인넷 이전 데이터 영역

메인넷 이전에는 어카운트가 500만개이상인경우 평균 500TPS 미만의 성능을 보임. 스테이트 트라이 와 레벨디비 문제

## 메인넷 이후 성능

어카운트 개수가 많아도 평균 3000TPS 정도의 성능을 보임. 현재 싸이프레스는 더 높은 성능을 보임.

### 스테이트 트라이 노드 캐시(추가됨)

스테이트 트라이와 디비 매니저사이에서 스테이트 트라이의 노드를 캐시해주는 역할.

디스크 영역에 대한 접근을 줄여준다.

디비 매니저.....

...

즉, 캐시와 파티셔닝으로 해결함.

메인넷 이전에는 노드가 필요할 때마다 디스크 영역에 접근 => 높은 지연시간, 높은 성능

캐시레이어를 추가해 캐시미스가 거의 일어나지 않음.

### 파티셔닝

메인넷 이전에는 단일 레벨디비에 모든 데이터 저장함. 블록, 레싶, 스테이트를 다 가지고 있었는데

메인넷 이후 블록, 레싶, 스테이트를 분리하고, 스테이트에는 4개의 디파티션을 함.

블록 쓰기에 걸린 시간이 맥스 12초까지 걸렸었는데, 1,2초로 됨.

## 늘어나기만 하는 블록체인 데이터, 줄일 수 있는 방법은?

비대해진 스테이트 파티션. 최신 스테이트가 가장 중요.

최신이 아닌 데이터를 줄일 방법이 없을까?

### 가정

- 지나간 데이터요청은 많지 않다.
- 지나간 상태에 대한 요청을 처리할 수 있는 노드가 존재

### 해결해야 할 문제

1. 최신 상태를 계속 없데이트하면서 지나간 상태 데이터를 삭제해야함.

### 해결 방안

1. 특정 블록 넘버 기준의 스테이트 트라이를 new db에 쓰고, 이전에 사용하던 db를 삭제
2. 최신 상채 업데이트는 new db에만 써줌.

### 예

100번 블록 기준 스테이트를 새로운 파티션에 복제하고 작업함.

## 노드가 최신 블록을 따라갈 수 있게 하는 방법

올드를 리드온리로 ...

---

# ??

## 싸이프레스

0.11원 정도의 수수료. 즋시 완결성

### 서비스 체인

퍼블릭, 프라이빗, 컨소시엄. 싸이프레스와 인터렉션할 수 있는 독립된 블록체인

- 테스트용도: 자체 테스트. 메인넷, 테스트넷과 별도로
- 토큰전용 디비: 토큰 정보 관리에 최적화된 데이터벵이스
- 비용: 가스 부담이 될때
- 신뢰: 자체 블록체인이지만, 메인넷과 연결하여 신뢰를 얻음
- 보안: 체인 데이터를 공개하고 싶지 않을때, 네트워크 저근 권한을 한정하고 싶을때
- 성능: 높은 TPS가 요구되는 특정 서비스를 위해서
- 커스터 마이징

브릿지 컨트랙트 - 밸류 트랜잭션에서 중요

### 앵커링

- 서비스 체인의 신뢰확보를 위함.
- 주기적인 서비스 체인 블록의 주요 해시들을 메인체인에 기록

### 밸류 트랜스퍼

- 서비스 체인과 메인 체인간에 klay/kcp(klaytn compatible token)
- 메인체인 클레이는 브릿지 컨트랙트. 서비스체인의 브릿지 컨트렉트가 유저에게 전달

#### kct 전송

1. 어브로브, 리퀘스트.
2. 서비스 체인에서는 민트해서 유저에게 전달

확장하여 어프로브, 리퀫스트를 한번에 묶어서 전송 메소드를 만들었음.

#### 멀티시그니쳐

- 오퍼레이터 키 탈취시 브릿지 컨트랙트 자산이 위험해짐. 멀티시그로 다수의 오퍼레이터의 승인을 요구 할 수 있음

### 서비스 체인의 넥스트스탭

서비스 체인마다 브릿지 컨트랙트가 붙어야함. KLVM도 필요. 이에 대한 구조적인 문제 등을 해결하려함.

---

# 위메이드 트리

자산거래 등이 중심인게 대부분이었다.

하지만 게임의 핵심은 자산거래가 아니다.

컨텐츠가 중요하다. 컨텐츠를 블록체인에 연결하자.

멀티체인 아키텍쳐

데이터 무결성.

체인 하이어라키

---

### 클레이튼 API

클레이튼 어플리케이션

로드밸런서 만으로는 데이터 조회가 어려움.

공개 KEN만 사용해선 안정적으로 할 수 없음. 최소 한개 이상을 운영해야함.

액새스 토큰, ip 화이트리스트, 트래픽 쓰레숄드

---

### 루트원 비트베리가 그리는 블록체인 api 및 플랫폼 서비스

블록체인 서비스 api, 토큰 간편스왑, 토큰 사용 채널

비트베리 커넥트, 비트베리 에어, 비트베리 페이

---

# 클레이튼 블록체인 어플리케이션 개발

### 최신 Bapp 동향

- NFT: 유일성, 소유권
- DID: 자기 주권 신원 블록체인 기반 모바일 전자증명

---

# 함수형 프로그래밍을 기반으로 한 Bapp 개발 사례 - 스핀프로토콜

ffp-js \* caver-js

generic-caver

---

# temco 온라인 마켓 플랫폼엣서 클레이튼 블록체인 활용

구하다. 명품온라인 마켓

상품 구매시 거의 3-40프로 취소나 반품이 남.

---

# 직토 - 클레이튼을 활용한 개인데이터의 효율적인 교환과 그 비용

인슈어리움

얼마야? 보험 대출

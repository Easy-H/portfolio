---
layout: portfolio_with_preview
tags: [개인 프로젝트, 게임]
thumbnail: HappyPlanet.png
summary: "🔧 Unity | Firebase&#10;🌟 시뮬레이션 게임&#10;🎮 상태: 완료"
preview: <iframe frameborder="0" src="https://itch.io/embed-upload/16444499?color=333333" allowfullscreen="" width="300" height="500"><a href="https://easy-h.itch.io/happy-planet">Play Happy Planet on itch.io</a></iframe>
social:
  - title: github
    info: Code
    url: https://github.com/team-prepper/happy-planet
  - title: itch-io
    info: Play
    url: https://easy-h.itch.io/happy-planet
---
<!-- card: 💡 게임 개요 -->

#### ✨ 장르
- 시뮬레이션
- 시간 조작

#### 📱 플랫폼
- WebGL

#### ⏰ 개발 기간
- 게임 플레이 : 2023-08-13 ~ 2024-06-19
- 소셜 네트워크 기능: 2024-06-19 ~ 2024-12-14
- 기타 리팩토링 및 유지보수: 2024-06-19 ~ 진행중

<!-- card: 💡 게임 개요 -->

#### 🛠 사용 도구
- Unity
- Firebase: 사용자 관리 및 플레이 데이터 클라우드 저장에 이용
    - Firestore
    - Firebase Realtime Database
    - Firebase Authentication
- EHTool: UI 관리, 언어 변경 기능에 이용

#### 👤 담당
- 전체 시스템 설계 및 개발
- UI 설계
- Firebase 연동

<!-- card: 📖 게임 소개  -->

**Happy Planet**은 다양한 유닛을 배치하고 시간의 흐름을 조작하며 자원을 관리하는 시뮬레이션 게임입니다.

행성을 직접 회전시켜 시간을 조작할 수 있으며, 이로 인해 유닛의 행동과 결과가 실시간으로 변화합니다.  

- 정방향 시간: 유닛이 작동하여 자원 생성  
- 역방향 시간: 과거 상태로 회귀하여 모든 행동과 자원이 되돌아감

<!-- card: 🛠️ 주요 기능 및 기여 -->

### ⏰ 시간 역행/재실행 시스템 구현(재화)
- 행성 회전 방향에 따라 게임 시간 변화
    - 정방향 회전: 게임 시간이 정방향으로 흐름
    - 역방향 회전: 게임 시간이 역방향으로 흐름
- 게임 시간에 따른 재화 회수, 획득
    - 유닛에 생성 시간, 마지막 재화 획득 시간, 재화 획득에 필요한 시간, 수명 저장
    - 현재 게임 시간이 마지막 재화 획득 시간보다 빠르다면 재화 획득 취소
    - 현재 게임 시간이 마지막 재화 획득 시간 + 재화 획득에 필요한 시간보다 느리다면 재화 획득
    - 수명이 만료된 유닛은 재화 생산 정지

<!-- card: 🛠️ 주요 기능 및 기여 -->

### ⏰ 시간 역행/재실행 시스템 구현(이벤트)
- 유닛 생성, 레벨 업, 삭제 이벤트를 로그 형태로 기록
- 데이터베이스 복구 시스템(WAL) 방식을 이용하여 이벤트 재실행, 취소 기능 구현
    - 마지막 로그 발생 시간이 현재 게임 시간보다 늦는 경우 이벤트 취소
    - 마지막 로그 취소의 기존 발생 시간이 현재 게임시간보다 빠른 경우 이벤트 재실행
- 새로운 로그가 기록될 때 로그 취소 기록을 삭제
- 재화 획득은 로그에 기록되지 않음
    - 중복 발생 방지
    - 재화 획득을 로그 기록에 배제함으로써 공간 비용, 저장 시간 비용 절약
        - 재화 획득의 발생 빈도가 더 잦음

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 🚀 행성 이동
- IPlayground 인터페이스를 통해 행성 소유자에 따라 다른 조작을 제공
- 행성 소유자와 접근자가 동일한 경우 행성 조작이 가능한 `Playground` 제공
    - 사용자는 독립된 유닛, 자원, 상태를 가지는 행성을 여러 개 보유 가능
- 행성 소유자 UID와 접근자가 동일하지 않을 경우 행성 조작이 불가능한 `Playground` 제공
    - 다른 유저의 UID를 입력해 해당 유저의 행성 관람 가능
    - 데이터베이스에서도 행성 소유자 UID와 접근자의 UID를 비교하여 다른 경우 읽기 권한만 부여
        - 소유자가 아닌 접근자가 행성에 변화를 가하는 것을 이중 방지

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 📱 크로스 플랫폼 데이터 관리 시스템 설계
- 사용자 로그인 및 게임 데이터를 Firebase를 이용하여 관리
    - Unity Firebase SDK가 WebGL 빌드에 작동하지 않는 문제를 해결하기 위해 jslib를 개발하여 WebGL 환경에서도 작동하도록 구현
- 로그인하지 않은 사용자의 데이터는 로컬에 JSON 형태로 저장하여 오프라인 플레이 지원
- 플랫폼(로컬, Firebase, WebGL Firebase)에 관계없이 로그인, 데이터를 일관적으로 접근할 수 있도록 `IAuth`, `IDatabaseConnector` 인터페이스를 설계
    - 시스템의 확장성, 유지보수성 확보

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 📋 `ScriptableObject`를 활용한 유닛 데이터 관리
- 싱글톤 패턴으로 구현한 UnitManager를 통해 모든 유닛에 대한 일관된 접근 포인트 제공
    - 데이터 관리의 효율성 증대
- 유닛의 아이콘, 이름, 설명, 레벨에 따른 재화 획득 정보를 `ScriptableObject`로 관리
    - 런타임 시 불필요한 메모리 할당을 줄임
    - 디자이너, 기획자가 코드 수정 없이 유닛 데이터를 손쉽게 생성, 수정 가능

<!-- card: ☁️ Firebase 연동 구조 -->

### 🔐 Firebase Authentication

- 유저는 Firebase 인증을 통해 식별됨
- UID를 기반으로 행성 및 데이터 기록

### 📁 Firestore

- 이벤트 로그 저장  
    - 예: `"users"/{UID}/log/{PlanetID}/`
- 각 로그는 유닛 변경 이벤트만 포함 (자원 획득 제외)

### 📡 Realtime Database

- `/metadata/{UID}/{PlanetID}`에 현재 게임 시간 및 자원 상태 저장
- 행성의 재화 정보, 시간 정보를 저장
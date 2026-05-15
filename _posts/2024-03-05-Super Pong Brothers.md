---
layout: portfolio_with_preview
tags: [개인 프로젝트, 게임]
thumbnail: SuperPongBros.png
summary:  "🔧 Unity | Firebase&#10;🌟 벽돌깨기, 슈팅&#10;🎮 상태: 완료"
preview: '<iframe frameborder="0" src="https://itch.io/embed-upload/15313913?color=333333" allowfullscreen="" style="aspect-ratio: 0.45"><a href="https://easy-h.itch.io/superpongbros">Play Super Pong Brosthers on itch.io</a></iframe>'
social:
    - title: github
      info: Code
      url: https://github.com/Easy-H/Break-Out
    - title: itch-io
      info: Play
      url: https://easy-h.itch.io/superpongbros
---
<!-- card: 💡 게임 개요 -->

### ✨ 장르
- 벽돌깨기 + 슈팅

### 📱 플랫폼
- WebGL

#### ⏰ 개발 기간
- 게임 플레이 : 2022-01-24 ~ 2023-10-13
- 랭킹 시스템: 2023-11-10 ~ 2024-03-09
- 기타 리팩토링 및 유지보수: 2024-03-12 ~ 진행중

<!-- card: 💡 게임 개요 -->

### 🛠 사용 도구
- Unity
- Firebase: 스코어 보드 기능에 이용
- EHTool: UI관리 기능에 이용

### 👤 담당
- 게임 기획
- 프로그래밍

<!-- card: 📖 게임 소개 -->

**Super Pong Brothers**는 벽돌깨기와 슈팅 게임을 융합한 아케이드 스타일의 점수 경쟁 게임입니다.  
총알을 쏘는 적을 공으로 맞추어 쓰러뜨리는 것이 기본적인 전투 방식입니다.

- **모든 공을 떨어뜨리면 피해를 입음**  
- 반대로, **피해를 입으면 공이 추가로 발사**되어 전략적으로 피해를 활용할 수 있음  
- 항상 하나 이상의 공이 필드에 있도록 설계된 시스템으로 **공 = 생존 리소스**라는 콘셉트 확립

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 📦 오브젝트 풀을 이용한 비용 절약
- 싱글톤 패턴을 이용하여 `ObjectPoolManager` 프리팹 관리
- 사용이 끝난 프리팹을 코드에 따라 `Dictionary` 자료구조에 저장
- 프리팹을 요청하는 경우 `Dictionary`에 존재하는 지 확인 후 생성된 프리팹/생성한 프리팹을 반환
- 프리팹 생성 비용 절약을 통한 성능 개선

### 📜 퀘스트, 페이즈 시스템 구현
- 점수가 일정 이상일 경우 퀘스트 달성 및 다음 페이즈로 전환
	  - 퀘스트 조건을 인터페이스로 추상화 및 구현
- 페이즈에 따라 등장하는 적 종류 및 적 수 변화
- `ScriptableObject`를 이용하여 퀘스트 조건, 페이즈 데이터 분리 관리
	  - 게임 밸런스를 코드 수정 없이 빠르게 조정 가능
  
<!-- card: 🛠️ 주요 기능 및 기여 -->

### 🎯 스코어 보드 및 랭킹 관리
- 게임 종료 후 Firebase Realtime Database에 점수 저장
- 플랫폼(로컬, Firebase, WebGL Firebase)에 관계없이 데이터를 일관적으로 접근할 수 있도록 `IDatabaseConnector` 인터페이스를 설계
    - 시스템의 확장성, 유지보수성 확보
---
layout: portfolio_with_preview
tags: [팀 프로젝트, 게임]
thumbnail: the-sixth-legend.png
summary: "🔧 Unity | Photon&#10;🌟 턴제 RPG&#10;🎮 상태: 완료"
preview: '<iframe frameborder="0" src="https://itch.io/embed-upload/16453574" allow="autoplay; fullscreen" style="aspect-ratio: 1.6"><a href="https://easy-h.itch.io/the-sixth-legend">Play The Sixth Legend on itch.io</a></iframe>'
social:
  - title: github
    info: Code
    url: https://github.com/Team-Prepper/Project_SWENG/tree/Modularization
  - title: itch-io
    info: Play
    url: https://easy-h.itch.io/the-sixth-legend
---
<!-- card: 💡 게임 개요 -->


### ✨ 장르
- 턴제 RPG
- 멀티 플레이

### 📱 플랫폼
- WebGL

#### ⏰ 개발 기간
- 게임 플레이 : 2023-09-06 ~ 2023-12-07
- 기타 리팩토링 및 유지보수: 2024-03-26 ~ 진행중

<!-- card: 💡 게임 개요 -->

### 🛠 사용 도구
- Unity
- Photon Network: 멀티플레이 구조 및 네트워크 플레이 환경
- EHTool: UI 관리, 언어 변경 기능에 이용

### 👤 담당
- UI 설계
- 언어 변경 기능
- 리팩토링

<!-- card: 📖 게임 소개  -->

육각 타일 기반의 멀티플레이 턴제 RPG 게임입니다.

턴을 시작할 때 주사위를 굴려 포인트를 얻은 뒤, 얻은 포인트를 활용하여 이동, 공격을 수행합니다.

멀티플레이 구조는 Photon Network를 사용하여 구성했습니다.

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 🔥 리팩토링: 캐릭터와 캐릭터 조작 인터페이스 분리
- 개선 전: 캐릭터 조작이 Photon Network에 종속됨
	- 캐릭터의 정보를 Photon Network를 이용하여 관리
	- Photon Network에 접속하지 않는 경우 플레이 불가능
		- 로컬 플레이 기능을 제공하기 위해서는 새로운 캐릭터 클래스 필요
- 개선: 캐릭터 조작 인터페이스(`ICharactorController`)에서 캐릭터 상태정보 관리
	- 상태 정보: 캐릭터 위치, 장비, 체력, 능력치 등
	- 로컬 플레이의 경우 캐릭터 상태 정보를 `LocalCharacterController`에서 관리
	- 네트워크 플레이의 경우 캐릭터 정보를 `PhotonCharacterController` 클래스에서 PhotonNetwork를 이용하여 관리
	- 새로운 캐릭터 클래스 없이 로컬 플레이 및 네트워크 플레이 기능 제공
	- 로컬 플레이에서 서버 처리를 제거해 그에 비례하는 로컬 성능 개선 및 구조 단순화 달성

<!-- card: 🛠️ 주요 기능 및 기여 -->
### 🔥 리팩토링: 캐릭터 조작 방식의 분리 및 유연성 확보
- 개선 전: 캐릭터에 조작 방식이 통합
	- AI 캐릭터는 AI에 의해서만 조작, 사용자 조작 캐릭터는 사용자에 의해서만 조작
	- 적 캐릭터와 플레이어블 캐릭터가 분리
- 개선: 캐릭터 행동 선택 인터페이스(`IActionSelector`)를 도입하여 캐릭터와 캐릭터의 행동 선택 방식을 분리
	- 전략 패턴을 적용
    - Character는 `IActionSelector`에 의해 조작
        - AI 캐릭터에는 `AISelector`가 할당
        - 사용자 조작 캐릭터에는 `GUIActionSelector`가 할당
	- 적 캐릭터로 지정되었던 캐릭터도 조작 가능해짐
		- 사용자 플레이 캐릭터 선택 구현이 가능해짐
      
<!-- card: 🛠️ 주요 기능 및 기여 -->
### 🔥 리팩토링: `ScriptableObject`를 이용한 캐릭터, 아이템 정보 관리
- 개선 전: 캐릭터 정보가 캐릭터 프리팹에 저장
	- 캐릭터, 아이템 정보 수정이 어려움
	- 캐릭터, 아이템 생성 시 불필요한 정보 포함 => 공간 비용 소모
- 개선: `ScriptableObject`를 이용한 캐릭터, 아이템 정보 관리
	- 캐릭터, 아이템 정보 수정 용의성 확보
	- 캐릭터, 아이템 생성 공간 비용 감소

### ✔️ 사용자 플레이 캐릭터 선택 구현
- 리팩토링에서 개선된 내용을 바탕으로 사용자 플레이 캐릭터 선택 구현

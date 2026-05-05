---
layout: portfolio_with_preview
tags: [개인 프로젝트, 게임]
thumbnail: CrossNumber.png
summary: "🔧 Unity | Firebase&#10;🌟 퍼즐&#10;🎮 상태: 완료"
preview: <iframe frameborder="0" src="https://itch.io/embed-upload/16444340?color=333333" allowfullscreen="" width="300" height="455"><a href="https://easy-h.itch.io/crossnumber">Play Cross Number on itch.io</a></iframe>
social:
  - title: github
    info: Code
    url: https://github.com/Easy-H/CrossNumber
  - title: itch-io
    info: Play
    url: https://easy-h.itch.io/crossnumber
---

<!-- card: 💡 게임 개요 -->

### ✨ 장르
- 수식 기반 퍼즐

### 📱 플랫폼
- WebGL

#### ⏰ 개발 기간
- 게임 플레이 : 2022-01-24 ~ 2023-11-22
- 맵 제작 시스템: 2023-03-18 ~ 2023-07-05
- 기타 리팩토링 및 유지보수: 2023-11-16 ~ 진행중

<!-- card: 💡 게임 개요 -->
### 🛠 사용 도구
- Unity
- Firebase: 로그인, 스테이지 공유 기능 구현에 이용
- EHTool: UI관리, 언어 변경 기능에 이용

### 👤 담당
- 게임 기획
- 프로그래밍

<!-- card: 📖 게임 소개 -->

**Cross Number**는 숫자와 연산 기호를 조작해 올바른 수식을 만드는 퍼즐 게임입니다.  
화면에 주어진 수식들이 모두 올바르게 되도록 퍼즐을 해결하면 클리어됩니다.

- **모든 수식의 오류를 수정하면 스테이지 클리어**
- 직관적 드래그 앤 드롭 인터페이스로 수식 수정
- 레벨 편집 및 공유 기능 탑재

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 🔢 유닛의 위치 제어 및 유닛 위치에 따른 스테이지 클리어 확인 기능
- 싱글톤 패턴을 이용한 `UnitManager`가 유닛 생성, 유닛 위치 관리
    - `Dictionary`를 이용하여 유닛의 위치 정보 저장
- 유닛의 정보는 `ScriptableObject`로 관리
- 스택을 이용하여 이동 경로 저장
- 씬에 놓인 유닛의 위치를 기반으로 수식의 결과 확인 및 클리어 확인
    - '=' 유닛의 상하의 계산식의 결과, 좌우의 계산식의 결과를 비교
		- 재귀 함수를 이용한 계산
    - 모든 유닛이 계산에 사용되는지 확인
    - 모든 유닛이 계산에 사용되고, 수식에 이상이 없다면 스테이지 클리어

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 📱 크로스 플랫폼 데이터 관리 시스템 설계
- 사용자 로그인 및 게임 데이터를 Firebase를 이용하여 관리
    - Unity Firebase SDK가 WebGL 빌드에 작동하지 않는 문제를 해결하기 위해 jslib를 개발하여 WebGL 환경에서도 작동하도록 구현
- 로그인하지 않은 사용자의 데이터는 로컬에 JSON 형태로 저장하여 오프라인 플레이 지원
- 플랫폼(로컬, Firebase, WebGL Firebase)에 관계없이 로그인, 데이터를 일관적으로 접근할 수 있도록 `IAuth`, `IDatabaseConnector` 인터페이스를 설계
    - 시스템의 확장성, 유지보수성 확보

<!-- card: 🛠️ 주요 기능 및 기여 -->

### ✍🏼 스테이지 제작 기능
- 선택한 유닛에 해당하는 유닛 생성
- 씬에 놓인 위치에 따라 유닛 데이터가 json으로 저장

### ➦ 스테이지 공유 기능
- 클리어 가능한 스테이지를 제작자가 플레이 하여 클리어 가능한지 확인하는 절차를 통해 확인
- 클리어 가능한 스테이지를 로그인 된 사용자가 업로드 한 스테이지의 개수가 4개 이하일 경우 데이터베이스에 등록
    - 데이터베이스는 `IDatabaseConnector`를 이용하여 접근

<!-- card: ☁️ Firebase Firestore 구조 -->
### 🧩 퍼즐 정보
- **MapId**와 **MapData**로 컬렉션을 나누어 저장
- **MapId**: 레벨을 식별하는 외부용 정보
- **MapData**: 실제 퍼즐 구성 데이터
### 👤 유저 시스템(예정)
- 추후 Firebase Authentication을 도입하여 구현
- UserData 컬렉션 추가
- 유저가 만든 MapId 코드 리스트 보관
- 맵 수정/삭제 권한 부여 가능
- 즐겨찾기, 추천, 신고 기능 확장 고려

<!-- card: ☁️ Firebase Firestore 구조 -->

### 📁 MapId 컬렉션
- 레벨을 식별하는 외부용 정보
- key-value 쌍으로 MapData의 위치와 이름을 보유

```plaintext
Collection: MapId
 └── Document ID: 랜덤 코드 (예: "X8PQ4")
       ├── key: "ABC123" ← MapData 문서 ID
       └── name: "곱셈 연습 맵"
```

<!-- card: ☁️ Firebase Firestore 구조 -->
### 📁 MapData 컬렉션
- 실제 퍼즐 구성 데이터
- 각 퍼즐 유닛을 번호(key)로 나열한 구조
```plaintext
Collection: MapData
 └── Document ID: ABC123
       ├── "0":
       │     ├── xPos: 0
       │     ├── yPos: 0
       │     └── Symbol: "*"
       ├── "1":
       │     ├── xPos: 1
       │     ├── yPos: 0
       │     └── Symbol: "5"
       └── ...
```

<!-- card: 🌱 회고 -->

- 실질적 사용자 제작 콘텐츠(UGC)를 구성하고 검증하는 시스템 설계 경험
- Firebase Firestore의 컬렉션/문서 기반 데이터 구조를 분리 설계하여 확장성 확보
- 익명 사용 환경에서의 데이터 식별 및 공유 흐름 설계
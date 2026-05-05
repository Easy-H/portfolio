---
layout: portfolio_with_preview
tags: [참여 프로젝트, 게임]
thumbnail: StudentSurvivor.jpg
preview: '<iframe frameborder="0" src="https://itch.io/embed-upload/9246182" allow="autoplay; fullscreen" style="width: 600px; height: 900px; transform: scale(0.5) translateX(-50%); /* 300/1980 */ transform-origin: top left; border: none;"><a href="https://rlatldnd1.itch.io/student-survivor">Play Student Survivor on itch.io</a></iframe>'
social:
  - title: github
    url: https://github.com/asdf-1256/Student_Survivor
  - title: itch-io
    url: https://rlatldnd1.itch.io/student-survivor
---
<!-- card: 💡 게임 개요 -->

### ✨ 장르
- 뱀서라이크

### 📱 플랫폼
- WebGL

#### ⏰ 개발 기간
- 게임 플레이 : 2023-11-15 ~ 2023-11-22
- 기타 리팩토링 및 유지보수: 2024-03-26 ~ 진행중

<!-- card: 💡 게임 개요 -->

### 🛠 사용 도구
- Unity

### 👤 담당
- 퀘스트 시스템 기획
- 퀘스트 시스템 및 보상 시스템 프로그래밍
- UI 시스템 프로그래밍

<!-- card: 📖 게임 소개 -->

컴퓨터공학과 학생이 대학 생활에서 살아남기 위해 과제, 시험, 출석과 싸우는 뱀서라이크 게임입니다.

수강 과목을 선택하고 해당 과목의 이수 조건(퀘스트)을 만족하여 능력치를 얻습니다.

<!-- card: 🛠️ 주요 기능 및 기여 -->

### 📜 퀘스트 시스템 기능 구현
- 싱글톤 패턴으로 구현된 `QuestManager`에서 각 퀘스트 조건 달성 여부를 확인 및 퀘스트 보상 수여
- 퀘스트 조건, 퀘스트 보상을 인터페이스로 추상화 및 구현
	- 퀘스트 조건 구현 예
		- 특정 적을 x마리 이상 처치
		- 체력을 x% 이하로 남기고 생존
		- x미터 이상으로 이동
	- 퀘스트 보상 예
		- 새로운 무기 획득
		- 이동속도 상승
	- 시스템의 확장성, 유지보수성 확보
- 퀘스트 정보를 `ScriptableObject`를 이용하여 저장
	- 데이터 수정, 생성의 용의성 확보

<!-- card: 🛠️ 주요 기능 및 기여 -->
## 🎨 UI 시스템 구현
- 싱글톤 패턴을 이용한 UI 시스템 구현
	- UI에 대해 일관된 접근 포인트 제공
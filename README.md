# 전주대학교x카카오엔터프라이즈 오프라인 현장강의 Track 5<br>n8n을 이용한 업무 자동화

> 예시 이미지 및 워크플로는 직접 작성하며, Apache2.0 라이선스에 따라 출처 표기 및 AI 학습에 이용을 금합니다.

### [WELCOME] n8n이란?
#### ● W-1. n8n 바로알기
&nbsp;&nbsp;– n8n은 `워크플로우 자동화` 도구  
&nbsp;&nbsp;– 각종 서비스를 코딩이 아닌 노드를 통해 연결하여 이벤트 발생 시 자동적인 처리가 진행되도록 해줌  
&nbsp;&nbsp;– [예시] 메일 자동화 : Gmail에 메일이 도착하면 내용을 요약해 사용자에게 알람 전송  

#### ● W-2. n8n 장단점  
&nbsp;&nbsp;– `클라우드 서비스 존재` : 복잡한 설치 없이 사용, 안정적인 서비스  
&nbsp;&nbsp;&nbsp;&nbsp; ㄴ 다만 유료이고, 검증된 노드만 사용 가능하므로 사용 가능한 노드 수가 로컬보다 적음  
&nbsp;&nbsp;– `오픈소스`이기 때문에 온라인서비스를 이용하지 않고도 로컬(개인컴퓨터) 또는 개인 서버(Docker/AWS)에서 서비스 구현이 가능  
&nbsp;&nbsp;– 로컬에서 데이터 통제가 가능  
&nbsp;&nbsp;– `JavaScript`와 `Python`을 사용해 비교적 쉬운 코드문법  
&nbsp;&nbsp;– 우리가 사용하는 `대부분의 앱(400+)과 API가 이미 n8n 내에 노드화`되어 있어 2차서비스 가공이 쉬움  
&nbsp;&nbsp;– 노드로 시각화되어 조건문, 루프문, 분기문 사용이 쉬움  
&nbsp;&nbsp;– `커뮤니티노드` 라이브러리 사용이 가능 (기본 노드의 부족한 기능들을 확장해줌, 신규기능)  
&nbsp;&nbsp;&nbsp;&nbsp; ㄴ npm 패키지 설치 또는 GUI 선택 설치  
&nbsp;&nbsp;&nbsp;&nbsp; ㄴ 클라우드버전에선 사용 불가 (2025부터 검증된 커뮤니티 노드는 설치 가능)  
&nbsp;&nbsp;&nbsp;&nbsp; ㄴ 커뮤니티 유저나 그룹이 만든 코드를 이용해야 하므로 코드지식(역공학)이 없는 경우엔 주의 요망 (숨겨진 코드 등으로 개인정보 탈취 우려)  
&nbsp;&nbsp;– `코드 노드`를 활용해 n8n에서 기본으로 지원하지 않는 기능도 구현 가능  

---

### [Section 01] n8n 기본기 다지기
#### ● 1-1. n8n 가입 및 메인페이지 접속
![n8n-home](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/00_n8n_%EC%B4%88%EA%B8%B0%ED%8E%98%EC%9D%B4%EC%A7%80.png)

#### ● 1-2. 새 워크플로 생성 및 UI 알아보기
&nbsp;&nbsp;① 홈 우측 상단의 'Create Workflow' 클릭  
&nbsp;&nbsp;② 워크플로 페이지 접속 (자동)  
![n8n-workflow-ui](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/01-n8n-workflow-ui.png)
&nbsp;&nbsp;– Execute workflow 버튼 : 현재 워크플로 일괄실행 버튼  
&nbsp;&nbsp;– 노드 테두리 색상 : Green 정상 실행 / Red 오류 발생  
&nbsp;&nbsp;– 노드 연결선 색상 : Green 정상 실행 / Gray 미실행  
&nbsp;&nbsp;– 메시지 알림창 : <오류, 성공, 힌트, 안내 등> 동작 중 알림사항이 팝업으로 출력되는 공간  

---

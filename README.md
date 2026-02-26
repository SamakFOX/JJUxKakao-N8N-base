# 전주대학교x카카오엔터프라이즈 오프라인 현장강의 Track 5<br>n8n을 이용한 업무 자동화

> 예시 이미지 및 워크플로는 직접 작성하며, MIT 또는 CCBY 라이선스에 따라 수정&배포 시 출처를 표기해주시고, AI 학습에 이용을 금합니다.

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

> 요약  
> GUI로 노드 조립을 통해 자동화를 구성해 쉽게&코드를 몰라도 자동화 서비스를 만들 수 있음  
> 무료로 사용 가능(로컬 또는 서버)  
> 400개 이상의 앱을 노드 하나로 연결 (Google, Github, MS, Notion, Slack 등)  

### ● W-3. n8n의 데이터 전달 방식  

&nbsp;&nbsp;– n8n은 노드간 데이터를 `JSON`으로 전달  
&nbsp;&nbsp;– JSON은 Key:Value 의 한 쌍으로 값이 전달되고 Key를 이용해 파싱  
&nbsp;&nbsp;[예시]  
```json
{
  "resultCode": "00",
  "resultMsg": "NORMAL_SERVICE",
  "numOfRows": 5,
  "pageNo": 1,
  "totalCount": 1,
  "data": [
    {
      "stn_id": 21229,
      "stn_ko": "울릉도",
      "va_val_02": 7.1,
      "va_val_03": "01",
      "va_val_04": 10
    },
    {
      "stn_id": 22101,
      "stn_ko": "덕적도",
      "va_val_02": 2.5,
      "va_val_03": "01",
      "va_val_04": null
    }
  ]
}
```
### ● W-4. n8n 주요 노드  

&nbsp;&nbsp;① Trigger 노드 : 워크플로를 시작 조건 (수동/자동)  
&nbsp;&nbsp;② Set 노드 : 새 데이터 생성 / 기존 데이터에 정보 추가  
&nbsp;&nbsp;③ Merge 노드 : 데이터 결합 (Append/Combine)  
&nbsp;&nbsp;④ IF 노드 : 조건을 통한 분기 처리  
&nbsp;&nbsp;⑤ OAuth 노드 : API 또는 서비스 접근 시 인증 처리  

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
&nbsp;&nbsp;– Publish 웹에서 접속할 수 있도록 서비스 발행 (취소는 햄버거메뉴의 Unpublish 클릭)

---

| [실습 1] Set & IF 기초 |
|---|

&nbsp;&nbsp;– 내 이력서 바탕으로 채용공고의 모집조건에 적합한지 확인 및 처리 자동화  

![n8n-p1-workflow](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/03-prac1-01_workflow.png)
<details>
    <summary>▶️ 자세히보기</summary>
    <br>
  
**① Edit Fields (Set) 노드로 예시데이터 수동입력 **  
![n8n-p1-setnode](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/04-prac-01_edit-fields_node.png)
![n8n-p1-setedit1](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/05-prac-01_edit-fields_edit1.png)
![n8n-p1-setedit1](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/06-prac-01_edit-fields_edit2.png)

**② Merge 노드로 데이터 병합 (전처리)**  
![n8n-p1-mergenode](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/07-prac-01_merge_node.png)
![n8n-p1-mergeedit](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/08-prac-01_merge_edit.png)

**③ If 노드로 조건 판별**  
![n8n-p1-ifnode](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/09-prac-01_if_node.png)
![n8n-p1-ifedit](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/10-prac-01_if_edit.png)

 - 필수 역량을 전부 갖춰야 하는 경우  
```JavaScript
{{ 
  Array.isArray($json["보유 역량"]) &&
  Array.isArray($json["필수 역량"]) &&
  $json["필수 역량"].every(r => $json["보유 역량"].includes(r))
}}
```
 - 필수 역량 중 하나만 갖추면 되는 경우  
```JavaScript
{{ 
  $json["필수 역량"].some(r => $json["보유 역량"].includes(r))
}}
```

**④ Edit Fileds (Set) 노드로 결과 단순확인 (후처리)**  

</details>

---

#### ● 1-3. OAuth 2.0 이란?  

&nbsp;&nbsp;– OAuth는 회원가입 없이 인증된 웹서비스를 이용해 인증을 거치는 방식  
&nbsp;&nbsp;– A 사이트에서 인증된 B사이트로 요청을 보내면 B에서 검증 후 확인값과 기본정보를 보내줌  
&nbsp;&nbsp;– A 사이트 이용 가능, 미이용 시 B사이트에서 연동 해제 가능  

---

| [실습 2] Google Sheet API 기초 |
|---|

&nbsp;&nbsp;– 구글시트 API노드를 이용한 데이터 입력 & 로드  

![n8n-p2-workflow](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/11-prac-02_workflow.png)

<details>
    <summary>▶️ 자세히보기</summary>
    <br>
  
**① 구글시트에서 데이터 불러오기**  
&nbsp;&nbsp;– 신규노드에서 Google Sheets 검색 후 Get row(s) in sheet 선택  
&nbsp;&nbsp;– Credential tot connect with를 클릭해 연결할 계정 설정 (없으면 로그인)  
&nbsp;&nbsp;– 연결된 계정의 구글드라이브로 공유받은 문서를 Document 리스트에서 선택  
&nbsp;&nbsp;– 선택된 Doc에서 이용할 시트명을 Sheet 리스트에서 선택   
![n8n-p2-gsmenu1](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/12-prac-02_gsheet-menu.png)  
![n8n-p2-gs_getrow1](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/13-prac-02_gs_getrow1.png)  
![n8n-p2-gs_getrow2](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/14-prac-02_gs_getrow2.png)  

**② 불러온 데이터 처리**  
&nbsp;&nbsp;– 설정값 중 Execute Once 토글  
&nbsp;&nbsp;&nbsp;&nbsp; ㄴ 기본설정으로는 10개의 데이터가 들어오면 10번 동작하도록 되어있으므로 1번만 동작하도록 변경  
&nbsp;&nbsp;– 임의 조작 (ex. 입력 데이터가 몇개인지와 확인한 시간을 출력)  
![n8n-p2-gs_readline](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/15-prac-02_edit-field_readline.png)  
```JavaScript
// 데이터 길이(갯수) 출력 명령
{{ $input.all().length }}

// 현재 시간 출력 명령
{{ $now.format('yyyy-MM-dd HH:mm:ss') }}
```

**③ 데이터 입력을 위한 샘플데이터 준비 (수동)**  
&nbsp;&nbsp;– 작업할 대상시트의 필드명과 입력할 타이틀명이 일치해야 제대로 입력됨  
&nbsp;&nbsp;&nbsp;&nbsp; ㄴ 다를 시 자동입력 과정에서 필드가 추가되며 포맷이 망가짐  
![n8n-p2-gs_sampledata](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/16-prac-02_edit-field_sampledata.png)  

**④ 구글시트로 데이터 입력**  
&nbsp;&nbsp;– 신규노드에서 Google Sheets 검색 후 Append row in sheet 선택  
&nbsp;&nbsp;– 작업할 계정, Document, Sheet를 정확히 선택  
&nbsp;&nbsp;– 자동입력을 원하면 Map Automatically 선택  
![n8n-p2-gsmenu2](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/17-prac-02_gsheet-menu.png)  
![n8n-p2-gs_appendrow](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/18-prac-02_gs_input.png)  

</details>

---

| [실습 3] Google Sheet API 응용 |
|---|

&nbsp;&nbsp;– 폼에서 입력을 받아 구글시트로 저장하기  

![n8n-p3-workflow](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/19-p03_workflow.png)

<details>
    <summary>▶️ 자세히보기</summary>
    <br>
  
**① 폼 생성하기**  
![n8n-p3-makeform](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/20-p03_makeform.png)
![n8n-p3-formdata-pin](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/21-p03_formdata_pin.png)
**② 폼 데이터를 구글시트로 입력하기**  
![n8n-p3-workflow](https://github.com/SamakFOX/JJUxKakao-N8N-base/blob/main/images/22-p03_formdata_input.png)

</details>

---

#### ● 1-4. Web-Hook Call Trigger  

&nbsp;&nbsp;※ 웹훅(Web-Hook) 이란?  
&nbsp;&nbsp;&nbsp; – 이벤트가 발생하면 미리 정해둔 URL로 데이터를 전송  

&nbsp;&nbsp;※ On Webhook call 노드  
&nbsp;&nbsp;&nbsp; – 웹 소켓을 열어두고 외부에서 HTTP 요청이 들어오면 워크플로를 실행  


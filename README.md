# 제주라는 교과서 — Interactive Workbook (Google 제출 내장형)

2026학년도 2학년 학생주도 자율자치 프로젝트 · 제주도 수학여행 연계 독서 기반 진로 융합 탐구 워크북입니다.
학생이 브라우저에서 바로 작성하고, 버튼 한 번으로 Google Spreadsheet에 제출합니다.

## 사용 방법

- **바로 열기**: `index.html` 을 브라우저로 엽니다.
- **웹으로 배포(GitHub Pages)**: 저장소 `Settings → Pages → Branch: main / root` 로 설정하면
  `https://<GitHub아이디>.github.io/jeju-as-textbook/` 주소로 학생에게 배포할 수 있습니다.

## 기능

- 9쪽 워크북. 각 칸에 입력하면 **이 기기(브라우저)에 자동 저장**됩니다(localStorage).
- 현장 사진 업로드(자동 압축 후 IndexedDB 저장), 현장 미션 체크.
- **`Google 제출`** 버튼 → 작성 내용·미션·사진을 Google Apps Script 웹앱으로 전송 → Google Spreadsheet에 기록.
- `작성내용 보기`(요약), `PDF/인쇄` 지원.

## 제출 주소(Apps Script) 바꾸기

`index.html` 안의 다음 줄을 본인 배포 주소로 교체하세요.

```js
const HARDCODED_APPS_SCRIPT_URL = "https://script.google.com/macros/s/.../exec";
```

Apps Script는 **배포 → 웹 앱 → 액세스 권한: 모든 사용자** 로 배포해야 학생 기기에서 제출됩니다.
`doGet` 은 `?ping=1` 요청에 `ok` 를, `doPost` 는 JSON 본문(`action:"submitWorkbook"`)을 받아 시트에 append 하도록 작성합니다.

## 유의 사항

- 제출 주소가 HTML에 그대로 들어가는 방식(주소 내장형)이므로, 공개 저장소에 올리면 Apps Script 웹앱 주소도 공개됩니다.
  웹앱은 입력을 받아 시트에 추가만 하고 시트 내용을 반환하지 않도록 작성하고, 스팸 방지가 필요하면 간단한 공유 키를 payload에 추가하세요.
- 학생 입력은 제출 전까지 해당 브라우저에만 저장됩니다. 기기를 바꾸거나 방문 기록을 지우면 사라집니다.
- 사진·이름 등 개인정보가 전송되므로, 학생·보호자 안내 및 시트 접근 권한 관리를 함께 진행하세요.

## 구성

```
jeju-as-textbook/
├─ index.html     # 워크북 본문 (페이지 이미지 + 입력 필드 + 제출 스크립트, 약 23 MB)
├─ .nojekyll      # GitHub Pages가 파일을 그대로 서빙하도록
└─ README.md
```

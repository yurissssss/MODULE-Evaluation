# 👩‍💻 프론트엔드 모듈 평가

---

## 🎯 프로젝트 개요

### 📌 달성 목표

- **Vue 3 기반 SPA 웹 애플리케이션 개발 능력** 확인
- **REST API** 통신 및 활용 능력 점검

### 📝 평가 방법

- 평가 문항에 따라 기본 프로젝트 구조 설계
- **Vue Router** 기반 CRUD 페이지 구현 필수

### 💻 기술 요구사항

- **Composition API** 기반의 컴포넌트 작성
- **vue-router**를 이용한 라우팅 처리
- **axios**를 활용한 REST API CRUD 요청\*\*

---

## 문제 1️⃣

> ### 프로젝트 기본 세팅

- [x] 프로젝트명: `contacts-app`
- [x] [추가모듈] bootstrap 5 설치
- [x] [추가모듈] axios 설치
- [x] [추가모듈] vue Router 설치
- [x] vite.config.js에 백엔드 서버 프록시 설정  
       `/api/contacts` 호출 → `http://localhost:3000/contacts`로 자동 변환
- [x] src/assets/main.css 초기화 후 fontAwesome css cdn을 import
      `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css`

---

## 문제 2️⃣

> ### 백엔드 환경 구축

- json-server 모듈을 이용하여 주어진 contacts.json을 데이터베이스 파일로 운영
- 엔드포인트: localhost:3000/contacts
- contacts.json은 공유 폴더에서 다운로드하여 사용
- 프로젝트 루트 폴더에 contacts.json 작성

---

## 문제 3️⃣

> ### 라우터 모듈 & 페이지 구성

|     | 페이지                | URL                    | URL name        | 컴포넌트               |
| --- | --------------------- | ---------------------- | --------------- | ---------------------- |
| ✅  | 첫 페이지             | `/`                    | home            | /contacts로 리다이렉트 |
| ✅  | 목록 보기 페이지      | `/contacts`            | contacts        | ContactListPage.vue    |
| ✅  | 상세 보기 페이지      | `/contacts/detail/:id` | contacts/detail | ContactDetailPage.vue  |
| ✅  | 새 연락처 추가 페이지 | `/contacts/write`      | contacts/write  | ContactWritePage.vue   |
| ✅  | 연락처 수정 페이지    | `/contacts/edit/:id`   | contacts/detail | ContactEditPage.vue    |

- 페이지 컴포넌트는 타이틀만 가지는 기본 페이지로 작성 후 추후 페이지 완성
- `/` 요청 시 `/contacts` 로 리다이렉트

```js
{
  path: '/',
  name: 'home',
  redirect: '/contacts',
}
```

---

## 문제 4️⃣

> ### ContactListPage.vue

- [x] api url: `[GET]/api/contacts`
- [x] 백엔드로부터 데이터를 다운받은 후 표로 출력하며, name 앞에 photo 출력
- [x] name을 클릭하면 상세보기로 이동
- [x] 새 연락처 버튼을 누르면 새 연락처 추가 페이지로 이동

🎨 Fontawesome 아이콘

- 연락처 : `fa-solid fa-address-book`
- 새 연락처 : `fa-solid fa-pen-to-square`

🚨 이미지는 시간이 걸리거나 깨질 수 있음

---

## 문제 5️⃣

> ### ContactDetailPage.vue

- [x] api url: `[GET]/api/contacts/:id`
- [x] 모든 정보를 출력
- [x] 목록 버튼을 누르면 목록 보기 페이지로 이동
- [x] 수정 버튼을 누르면 수정 페이지로 이동
- [x] 삭제버튼을 누르면 해당 연락처 삭제 후 목록 보기 페이지로 이동
- 삭제 전 사용자에게 확인 받기
- api url: `[DELETE]/api/contacts/:id`

🎨 Fontawesome 아이콘

- 연락처 아이콘: `fa-solid fa-address-book`
- 목록 아이콘: `fa-solid fa-list`
- 수정 아이콘: `fa-solid fa-pen-to-square`
- 삭제 아이콘: `fa-solid fa-trash-can`

🚨 이미지는 시간이 걸리거나 깨질 수 있음

---

## 문제 6️⃣

> ### ContactWritePage.vue

- [x] api url: `[POST]/api/contacts`
- [x] 부트스트랩을 이용하여 입력폼 구성
- [x] 확인 버튼을 누르면 저장할 지 사용자에게 확인 받고, 서버에 추가
- 성공 시 목록 보기 페이지로 이동
- [x] 취소 버튼을 누르면 목록 보기 페이지로 이동

🎨 Fontawesome 아이콘

- 새 연락처 : `fa-solid fa-pen-to-square`
- 확인 : `fa-solid fa-check`
- 취소 : `fa-solid fa-rotate-left`

🚨 name, tel은 필수 입력 요소 ➡️ 두 항목에 대한 입력 여부를 확인 후 전송하도록 함

---

## 문제 7️⃣

> ### ContactEditPage.vue

- [x] api url: `[PUT]/api/contacts/:id`
- [x] 부트스트랩을 이용하여 입력폼 구성
- [x] 백엔드로부터 해당 id에 해당하는 정보를 다운받아, 폼 입력요소들을 초기화
- [x] 확인 버튼을 누르면 저장할 지 사용자에게 확인 받고, 서버로 전송
- 성공 시 목록 보기 페이지로 이동
- [x] 취소 버튼을 누르면 목록 보기 페이지로 이동

🎨 Fontawesome 아이콘

- 새 연락처 : `fa-solid fa-pen-to-square`
- 확인 아이콘: `fa-solid fa-check`
- 취소 아이콘: `fa-solid fa-rotate-left`

🚨 name, tel은 필수 입력 요소 ➡️ 두 항목에 대한 입력 여부를 확인 후 전송하도록 함

---

> 작성자: 신유리
> 작성일: 2025.04.20  
> 모든 페이지 구성 완료 💯

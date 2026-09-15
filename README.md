# 오늘의 도장 — 다이어트 기록 앱

몸무게, 식단, 운동을 기록하고 표정 스티커를 붙이는 모바일 기록장입니다.
파이어베이스에 로그인하면 폰과 컴퓨터 등 여러 기기에서 같은 기록이 자동으로 동기화됩니다.

## 폴더 구성

- `index.html` — 앱 본체 (이 파일 하나가 앱 전체예요)
- `config.js` — 파이어베이스 설정을 넣는 곳 (여기만 수정하면 됩니다)
- `firestore.rules` — 파이어베이스 보안 규칙 (콘솔에 붙여넣을 내용)
- `README.md` — 이 안내서

---

## 준비: 왜 파이어베이스가 필요한가요

깃허브 페이지는 화면만 보여주는 곳이라 기록을 저장할 공간이 없어요.
그래서 무료 저장소인 파이어베이스를 하나 만들어 연결합니다.
한 번만 설정해두면 그 뒤로는 신경 쓸 일이 없어요.

`config.js`에 들어가는 값들은 공개돼도 안전합니다. 실제 보안은 로그인과 아래 보안 규칙이 담당해요.

---

## 1단계 — 파이어베이스 프로젝트 만들기

1. https://console.firebase.google.com 에 구글 계정으로 접속
2. **프로젝트 추가** → 이름 아무거나 (예: `dojang`) → 만들기 (구글 애널리틱스는 꺼도 됩니다)
3. 왼쪽 메뉴 **빌드 → Firestore Database** → **데이터베이스 만들기** → 위치는 그대로 → **프로덕션 모드**로 시작
4. 왼쪽 메뉴 **빌드 → Authentication** → **시작하기** → **이메일/비밀번호** 선택 → **사용 설정** 켜고 저장
5. 왼쪽 위 **프로젝트 개요 옆 톱니바퀴 → 프로젝트 설정** → 아래로 내려 **내 앱**에서 **`</>` (웹)** 아이콘 클릭 → 앱 이름 아무거나 입력하고 등록
6. 화면에 나오는 `firebaseConfig` 값을 복사 (apiKey, authDomain, projectId 등)

## 2단계 — config.js에 붙여넣기

`config.js` 파일을 열어서, 방금 복사한 값으로 `여기에_붙여넣기` 부분을 하나씩 바꿔주세요.

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "dojang-xxxx.firebaseapp.com",
  projectId: "dojang-xxxx",
  storageBucket: "dojang-xxxx.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcd..."
};
```

## 3단계 — 보안 규칙 넣기

1. 파이어베이스 콘솔 **Firestore Database → 규칙** 탭
2. `firestore.rules` 파일의 내용을 그대로 복사해 붙여넣기 → **게시**

이 규칙은 "로그인한 사람은 자기 기록만 읽고 쓸 수 있다"는 뜻이에요.

---

## 4단계 — 깃허브에 올리기

1. https://github.com 에서 **New repository** → 이름 (예: `dojang`) → **Public** 선택 → Create
   - 무료 계정은 깃허브 페이지를 쓰려면 Public이어야 해요. config.js 값은 공개돼도 안전하니 괜찮습니다.
2. 저장소 화면에서 **Add file → Upload files** → 이 폴더의 파일들(`index.html`, `config.js`, `firestore.rules`, `README.md`)을 끌어다 놓고 **Commit changes**

## 5단계 — 깃허브 페이지 켜기

1. 저장소 **Settings → Pages**
2. **Source**를 `Deploy from a branch`, 브랜치는 `main`, 폴더는 `/ (root)` → **Save**
3. 잠시 뒤 주소가 나와요: `https://내아이디.github.io/dojang/`

## 6단계 — 파이어베이스에 주소 허용하기

1. 파이어베이스 콘솔 **Authentication → Settings(설정) → 승인된 도메인**
2. **도메인 추가** → `내아이디.github.io` 입력하고 추가

---

## 사용하기

- 5단계에서 나온 주소를 폰 브라우저에서 열어요
- 처음이면 **회원가입**으로 이메일과 비밀번호를 만들고, 그다음부터는 **로그인**
- 컴퓨터나 다른 폰에서도 같은 이메일로 로그인하면 같은 기록이 보여요
- 폰에서 브라우저 메뉴의 **홈 화면에 추가**를 누르면 앱처럼 아이콘으로 열 수 있어요

## 참고

- 개인용 사용량은 파이어베이스 무료 한도 안에서 충분합니다
- 설정이 안 된 상태(config.js가 비어 있음)에서도 앱은 켜지지만, 그때는 그 기기에만 저장돼요
- 나중에 앱을 고치고 싶으면 이 대화로 돌아와 말씀해주세요

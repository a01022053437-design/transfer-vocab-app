# 편입 단어 — 모든 기기 자동 동기화

GitHub Pages로 화면을 제공하고, **Firebase Authentication + Cloud Firestore**로 단어와 학습 기록을 저장합니다. PC·iPhone·iPad 등에서 **같은 Google 계정으로 로그인하면 즉시 같은 데이터**를 봅니다. 앱은 Google 로그인을 하지 않으면 데이터를 저장하거나 표시하지 않습니다.

## 한 번만 설정하기 (약 10분)

1. [Firebase Console](https://console.firebase.google.com/)에서 프로젝트를 새로 만듭니다.
2. 프로젝트 개요의 웹 아이콘(`</>`)을 눌러 웹 앱을 추가하고, 표시되는 Firebase 설정값을 복사합니다.
3. 이 폴더의 `firebase-config.js`를 열어 복사한 설정값으로 `PASTE_...` 부분을 모두 바꿉니다. **서비스 계정 키는 절대 넣지 마세요.**
4. Firebase Console → **Authentication** → Sign-in method에서 **Google**을 활성화합니다.
5. Firebase Console → **Firestore Database**에서 데이터베이스를 만듭니다. 위치는 가까운 곳을 선택합니다.
6. Firestore의 **Rules** 화면에 `firestore.rules`의 내용을 전부 붙여 넣고 Publish합니다. 이 규칙은 로그인한 본인만 본인 단어에 접근하도록 제한합니다.
7. Authentication → Settings → Authorized domains에 GitHub Pages 주소의 도메인(예: `내아이디.github.io`)을 추가합니다. `localhost`는 개발용으로 기본 등록되어 있습니다.
8. 이 폴더의 파일을 GitHub 저장소 최상위에 올린 뒤 Settings → Pages에서 `main / (root)`를 배포 원본으로 선택합니다.

이후 각 기기에서 배포 주소에 접속해 **같은 Google 계정으로 로그인**하면 됩니다. 단어장 화면의 **+ 단어 추가**로 새 카드를 만들고, 각 카드의 **수정 / 삭제**로 자유롭게 관리할 수 있습니다. 단어 추가, 수정, 삭제, 복습 버튼, 오답 횟수와 다음 복습일은 모두 자동으로 저장·동기화됩니다.

## CSV 형식

```csv
word,meaning,part_of_speech,example,synonyms,related,tags
mitigate,완화하다,verb,The policy may mitigate the problem.,alleviate; reduce,mitigation,Day1;중요
```

`word`는 필수이며, 대소문자를 구분하지 않고 같은 단어는 자동으로 제외합니다. `tags`는 세미콜론(`;`)으로 여러 개를 입력합니다. 처음 로그인했을 때 `sample_words.csv`의 Day 1 예시 단어가 자동으로 저장됩니다.

## 백업

오른쪽 위 `•••` → **CSV 내보내기**로 전체 단어와 학습 진행 상태를 다운로드할 수 있습니다. 복원할 때는 빈 계정의 앱에서 CSV 가져오기를 사용하세요. 이미 있는 단어는 중복으로 추가되지 않습니다.

# Firebase 설정 가이드

개선된 향수 캘린더는 Firebase를 사용하여 로그인 및 클라우드 동기화 기능을 제공합니다.

## Firebase 프로젝트 만들기

### 1단계: Firebase 콘솔 접속
1. https://console.firebase.google.com/ 접속
2. Google 계정으로 로그인
3. "프로젝트 추가" 클릭

### 2단계: 프로젝트 생성
1. 프로젝트 이름: `perfume-calendar` 입력
2. "계속" 클릭
3. Google 애널리틱스: 원하는 대로 선택
4. "프로젝트 만들기" 클릭

### 3단계: 웹 앱 추가
1. 프로젝트 개요 페이지에서 `</>` (웹) 아이콘 클릭
2. 앱 닉네임: `향수 캘린더` 입력
3. "앱 등록" 클릭
4. **Firebase SDK 구성** 정보가 표시됩니다 - 이 정보를 복사하세요!

```javascript
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "perfume-calendar-xxxxx.firebaseapp.com",
  databaseURL: "https://perfume-calendar-xxxxx.firebaseio.com",
  projectId: "perfume-calendar-xxxxx",
  storageBucket: "perfume-calendar-xxxxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:xxxxx"
};
```

### 4단계: Authentication 설정
1. 왼쪽 메뉴에서 "Authentication" 클릭
2. "시작하기" 클릭
3. "Sign-in method" 탭 클릭
4. "Google" 클릭
5. "사용 설정" 토글 ON
6. 프로젝트 지원 이메일 선택
7. "저장" 클릭

### 5단계: Realtime Database 설정
1. 왼쪽 메뉴에서 "Realtime Database" 클릭
2. "데이터베이스 만들기" 클릭
3. 위치: "asia-northeast3" (서울) 선택
4. 보안 규칙: "테스트 모드에서 시작" 선택
5. "사용 설정" 클릭

### 6단계: 보안 규칙 설정
Realtime Database의 "규칙" 탭에서 다음 규칙으로 변경:

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    }
  }
}
```

"게시" 클릭

### 7단계: index.html 수정
1. `index.html` 파일 열기
2. 다음 부분을 찾기:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    // ...
};
```

3. 3단계에서 복사한 Firebase 구성 정보로 교체
4. 파일 저장

## Kakao 로그인 설정 (선택사항)

### 1단계: Kakao Developers 콘솔
1. https://developers.kakao.com/ 접속
2. Kakao 계정으로 로그인
3. "내 애플리케이션" 클릭
4. "애플리케이션 추가하기" 클릭

### 2단계: 앱 생성
1. 앱 이름: `향수 캘린더` 입력
2. 사업자명: 본인 이름 입력
3. "저장" 클릭

### 3단계: 플랫폼 등록
1. "플랫폼" 탭 클릭
2. "Web 플랫폼 등록" 클릭
3. 사이트 도메인: GitHub Pages 주소 입력
   예: `https://your-username.github.io`
4. "저장" 클릭

### 4단계: JavaScript 키 복사
1. "요약 정보" 탭에서 "JavaScript 키" 복사
2. `index.html` 파일에서 다음 부분 수정:

```javascript
Kakao.init('YOUR_KAKAO_JAVASCRIPT_KEY');
```

3. 복사한 JavaScript 키로 교체

## 완료!

이제 앱을 GitHub Pages에 업로드하고 사용할 수 있습니다.

## 주의사항

- Firebase 무료 플랜(Spark)으로 충분합니다
- 동시 접속자 100명까지 무료
- 데이터 저장 1GB, 다운로드 10GB/월 무료
- Kakao 로그인은 선택사항입니다 (Google만으로도 충분)

## 문제 해결

**로그인이 안 되는 경우:**
1. Firebase 콘솔에서 Authentication > Settings
2. "승인된 도메인"에 GitHub Pages 도메인 추가
   예: `your-username.github.io`

**데이터가 저장 안 되는 경우:**
1. Realtime Database 규칙 확인
2. 브라우저 콘솔(F12)에서 에러 확인

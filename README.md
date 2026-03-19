# Wini - 룸메이트 감정 커뮤니케이션 앱

> DND 13기 4팀 프론트엔드 프로젝트

룸메이트와 감정 편지를 주고받으며 서로의 마음을 이해하고 함께 성장하는 크로스플랫폼 모바일 앱입니다.

---

## 주요 기능

- **마음 편지 작성** - 감정 선택 → 상황/행동 → 약속 설정의 단계별 편지 작성 플로우
- **홈 화면** - 오늘의 편지, 룸메이트 상태, 통계 요약, 상태 메시지 관리
- **아카이브** - 저장된 편지 목록 및 상세 조회
- **통계** - 주간 감정 리포트, 성장 지표, 키워드 분석
- **룸메이트 매칭** - 초대 코드 기반 방 생성 및 연결
- **실시간 알림** - FCM(Firebase Cloud Messaging) 및 SSE(Server-Sent Events)

---

## 기술 스택

| 분류            | 기술                             |
| --------------- | -------------------------------- |
| Framework       | React Native 0.79.5, Expo 53     |
| Language        | TypeScript 5.8.3                 |
| Routing         | Expo Router 5 (파일 기반 라우팅) |
| 서버 상태       | TanStack React Query 5           |
| 클라이언트 상태 | Zustand 5                        |
| HTTP Client     | Axios 1.11                       |
| 인증            | Kakao OAuth, Apple Sign-In       |
| 푸시 알림       | Firebase Cloud Messaging         |
| 실시간 통신     | Server-Sent Events (SSE)         |
| 애니메이션      | React Native Reanimated 3        |
| 로컬 스토리지   | AsyncStorage                     |
| 폰트            | Pretendard                       |

---

## 시작하기

### 요구사항

- Node.js v22.18.0 (`.nvmrc` 참고)
- Expo CLI
- iOS 개발: Xcode (macOS 필요)
- Android 개발: Android Studio

### 설치

```bash
# 의존성 설치
npm install
```

### 환경 변수 설정

`.env.example`을 참고하여 `.env` 파일을 생성하세요.

```env
EXPO_PUBLIC_API_URL=https://app.wini.my
EXPO_PUBLIC_ENV=development
EXPO_PUBLIC_IS_MATCHED=false
EXPO_PUBLIC_SAMPLE_ACCESS_TOKEN=your_token_here
```

### 개발 서버 실행

```bash
# 플랫폼 선택 메뉴와 함께 시작
npm run start

# iOS 시뮬레이터
npm run ios

# Android 에뮬레이터
npm run android

# 웹 브라우저
npm run web
```

### 실기기 빌드

```bash
# iOS 실기기
npm run build:local:ios

# Android 실기기
npm run build:local:android
```

---

## 프로젝트 구조

```
dnd-13th-4-frontend/
├── app/                      # Expo Router 파일 기반 라우팅
│   ├── _layout.tsx           # 루트 레이아웃 (인증, 알림, 쿼리 초기화)
│   ├── (tabs)/               # 탭 네비게이션
│   │   ├── index.tsx         # 홈 화면
│   │   ├── Statistics.tsx    # 통계
│   │   ├── MyPage.tsx        # 마이페이지
│   │   ├── archive/          # 아카이브 (목록, 상세)
│   │   └── notes/            # 편지 작성 플로우
│   ├── matching/             # 룸메이트 매칭
│   └── onboarding/           # 온보딩 / 로그인
├── components/               # 재사용 UI 컴포넌트
├── hooks/                    # 커스텀 훅
│   └── api/                  # React Query 훅
├── lib/                      # 유틸리티 라이브러리
│   ├── api/                  # Axios 인스턴스 & 인터셉터
│   ├── auth/                 # 토큰 관리
│   └── notifications/        # FCM 설정
├── services/                 # 비즈니스 로직 (인증 서비스)
├── store/                    # Zustand 스토어
├── constants/                # 앱 상수 (컬러, 타이포그래피, API 경로)
└── types/                    # TypeScript 타입 정의
```

---

## 아키텍처

### 상태 관리 전략

- **React Query** - 서버 상태 (API 데이터 캐싱, 동기화)
- **Zustand** - 로컬 UI 상태 (편지 작성 폼, 토스트)
- **AsyncStorage** - 영속성 데이터 (인증 토큰)

### 인증 플로우

1. Kakao OAuth / Apple Sign-In으로 소셜 로그인
2. JWT Access Token + Refresh Token 발급
3. Axios 인터셉터를 통해 자동으로 Authorization 헤더 주입
4. 401 응답 시 Refresh Token으로 자동 토큰 재발급

### 탭 네비게이션

5개 탭: 홈 | 아카이브 | 작성(중앙 버튼) | 통계 | 마이페이지

---

## EAS 빌드 (배포)

```bash
# 개발 빌드
eas build --platform android --profile development
eas build --platform ios --profile development

# 스테이징
eas build --profile staging

# 프로덕션
eas build --profile production
```

---

## 코드 스타일

```bash
# 린트 검사
npm run lint
```

- ESLint (Expo config + TanStack Query plugin)
- Prettier (80자 줄 너비, 싱글 쿼트)
- TypeScript strict 모드

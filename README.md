# Twitch Clone

## 프로젝트 실행
- `npm run dev`
- `ngrok http --domain=national-utterly-beetle.ngrok-free.app 3000`

## Key Features:
- 📡 Streaming using RTMP / WHIP protocols 
- 🌐 Generating ingress
- 🔗 Connecting Next.js app to OBS / Your favorite streaming software 
- 🔐 Authentication 
- 📸 Thumbnail upload
- 👀 Live viewer count 
- 🚦 Live statuses 
- 💬 Real-time chat using sockets 
- 🎨 Unique color for each viewer in chat 
- 👥 Following system 
- 🚫 Blocking system 
- 👢 Kicking participants from a stream in real-time 
- 🎛️ Streamer / Creator Dashboard 
- 🐢 Slow chat mode 
- 🔒 Followers only chat mode 
- 📴 Enable / Disable chat 
- 🔽 Collapsible layout (hide sidebars, chat etc, theatre mode etc.) 
- 📚 Sidebar following & recommendations tab 
- 🏠 Home page recommending streams, sorted by live first 
- 🔍 Search results page with a different layout 
- 🔄 Syncing user information to our DB using Webhooks 
- 📡 Syncing live status information to our DB using Webhooks 
- 🤝 Community tab 
- 🎨 Beautiful design
- ⚡ Blazing fast application 
- 📄 SSR (Server-Side Rendering) 
- 🗺️ Grouped routes & layouts 
- 🗃️ MySQL
- 🚀 Deployment

# [Part 1](https://www.youtube.com/watch?v=a02JAryRPVU)
## Setup
- `npx create-next-app@latest twitch-clone`
```bash
✔ Would you like to use TypeScript? … No / Yes
✔ Would you like to use ESLint? … No / Yes
✔ Would you like to use Tailwind CSS? … No / Yes
✔ Would you like to use `src/` directory? … No / Yes
✔ Would you like to use App Router? (recommended) … No / Yes
✔ Would you like to customize the default import alias (@/*)? … No / Yes
```
- shadcn-ui 적용
  - npx shadcn-ui@latest init
  ```bash
  ✔ Would you like to use TypeScript (recommended)? … no / yes
  ✔ Which style would you like to use? › Default
  ✔ Which color would you like to use as base color? › Neutral
  ✔ Where is your global CSS file? … app/globals.css
  ✔ Would you like to use CSS variables for colors? … no / yes
  ✔ Are you using a custom tailwind prefix eg. tw-? (Leave blank if not) … 
  ✔ Where is your tailwind.config.js located? … tailwind.config.ts
  ✔ Configure the import alias for components: … @/components
  ✔ Configure the import alias for utils: … @/lib/utils
  ✔ Are you using React Server Components? … no / yes
  ✔ Write configuration to components.json. Proceed? … yes
  ```
  
### dependencies
- `npx shadcn-ui@latest add button`

## Authentication
- [Clerk](https://clerk.com/) 프로젝트 생성
  - gmail 만 사용
  - `.env` Clerk Key 추가
    - NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
    - CLERK_SECRET_KEY
    - .gitignore 에 .env 추가
- app/layout.tsx 수정
  - Root 에 Clerk Provider 추가
- middleware.ts 생성
  - 이제 Clerk 이 애플리케이션에 설치되어 마운트되었으므로, 어떤 페이지를 공개하고 어떤 페이지에 액세스하려면 인증이 필요한지 결정할 수 있습니다.
  - middleware.ts 파일을 생성합니다. 애플리케이션이 src/ 디렉터리를 사용하는 경우, middleware.ts 파일은 src/ 폴더 안에 위치해야 합니다. src/ 디렉터리를 사용하지 않는 경우, .env.local과 함께 루트 디렉터리에 middleware.ts 파일을 배치합니다.
  - 전체 애플리케이션이 보호 됩니다.
- [app/(auth) 생성](https://clerk.com/docs/references/nextjs/custom-signup-signin-pages)
  - sign-in 생성
  - sign-up 생성
  - [.env 에 환경 변수 추가](https://clerk.com/docs/references/nextjs/custom-signup-signin-pages#update-your-environment-variables)
    - 이 값은 사용자가 로그인하거나 가입할 때, 그리고 각 컴포넌트의 하단에 있는 각 링크를 클릭할 때 컴포넌트의 동작을 제어합니다.
- app/(auth)/layout.tsx 생성
  - Clerk UI Layout

### dependencies
- `npm install @clerk/nextjs`

### Notes
**[.env 에 환경 변수 추가](https://clerk.com/docs/references/nextjs/custom-signup-signin-pages#update-your-environment-variables)**
- 이 작업을 하지 않으면 Clerk 의 sign-in 으로 접속되므로 페이지를 커스텀해도 보이지 않게 되므로 커스텀한 페이지를 보여주려면 .env 에 path 입력을 해야 합니다.

## Dark mode
- app/globals.css 수정
  - 전체적으로 수정
- public/spooky.svg 이미지 추가
- app/(auth)/_components/logo.tsx 생성
  - 로그인 박스 위에 보여줄 로고 컴포넌트
- app/(auth)/layout.tsx 수정
  - 로그인 창에서 보여줄 layout 수정
- app/layout.tsx 수정
  - 테마적용
- Clerk - UserName 적용
  - Clerk > Dashboard > Project
  - User & Authentication > Email, Phone, Username
    - Username 활성화
    - 톱니바퀴 > Sign-in 비활성화

### dependencies
- `npm i @clerk/themes`
- `npm install next-themes`

### Note
**Clerk - UserName 적용 후 로그인 플로우**
1. 계정 로그인
2. 유저명 입력하는 창 노출
3. 유저명 입력 후 로그인

## Database setup
- 동영상에는 PlanetScale 을 사용하지만 mysql 로 대체

## Prisma
1. Prisma 설치
  - `npm i -D prisma`
2. Prisma 초기화
  - `npx prisma init`
  - prisma/schema.prisma 폴더와 파일이 생김
3. .evn 환경 변수 추가 `DATABASE_URL`
4. schema.prisma 설정
  - schema.prisma 모델 추가
  - `npx prisma generate`
  - `npx prisma db push`
  - `npm i @prisma/client`
  - `npx prisma studio` - 웹사이트로 prisma 스튜디오 열기

### MySQL 로컬 설치 및 로그인 (Mac OS 기준)
```bash
brew install mysql
```
- mysql 설치

```bash
brew services start mysql
...
==> Successfully started `mysql` (label: homebrew.mxcl.mysql)
```
- mysql 서비스 시작

```bash
brew services stop mysql
Stopping `mysql`... (might take a while)
==> Successfully stopped `mysql` (label: homebrew.mxcl.mysql)
```
- mysql 서비스 종료

```bash
mysql -uroot
```
- `-u` 옵션은 유저 이름을 지칭
- `root`는 기본 계정입니다. 해당계정으로 로그인하겠다는 것입니다. 
- 디폴트로는 비밀번호가 설정되어 있지 않은데, 비밀번호를 설정하고 싶으면 로그인 전에 아래처럼 입력해줍니다.
```bash
mysql_secure_installation
```

### MySQL 간단 명령어
```bash
mysql> status;
```
- mysql 연결 상태 정보

```bash
mysql> show databases;
```
- Database 리스트

```bash
mysql> CREATE DATABASE somedatabase;
```
- 데이터베이스 생성

```bash
mysql> select database();
```
- 현재 사용중인 데이터 베이스 조회

```bash
mysql> use somedatabase;
Database changed
```
- 데이터베이스 사용

- [Prisma Database Connector - MySQL](https://www.prisma.io/docs/concepts/database-connectors/mysql)

## Local tunnel
- ngrok 설치 및 설정

### [ngrok](https://ngrok.com/download) 설치
- ngrok 은 리버스 프록시, 방화벽, API 게이트웨이, 글로벌 로드 밸런싱을 결합하여 앱과 API를 제공합니다.
- `brew install ngrok/ngrok/ngrok`
- ngrok 회원가입 / 로그인 후 대시보드 진입
  - `ngrok config add-authtoken 2eZYdEQ8Hpe9JHsuJtRHk_iKUzA8Zg7KChaumVKMh2`
- `ngrok http 3000`
  ```bash
    Session Status                online                                    
    Account                       albert (Plan: Free)                       
    Version                       3.5.0                                     
    Region                        Japan (jp)                                
    Latency                       38ms                                      
    Web Interface                 http://127.0.0.1:4040                     
    Forwarding                    https://767f-118-33-142-61.ngrok-free.app
  ```
  - `https://767f-118-33-142-61.ngrok-free.app` https 로 접근
- ngrok > Dashboard > Cloud Edge > Domains > New Domain
  - Start a Tunnel > 커맨드 라인에서 tunnel 시작하기
  - `ngrok http --domain=national-utterly-beetle.ngrok-free.app 3000` 
  터미널에 입력
- Cloud Edge > Endpoints 로 들어가면 생성된 도메인 보이고 주소 복사가능
- 주소로 접속하면 localhost 가 아닌 도메인으로 표시 및 https 접속

## Clerk webhook
- Clerk Dashboard > Webhooks 에서 등록
  - Endpoint URL 추가 : https://national-utterly-beetle.ngrok-free.app/api/webhooks/clerk
  - Message Filtering > Filter events > user 필터링 > create
    - created, deleted, updated
- .env > `CLERK_WEBHOOK_SECRET=시크릿키 입력(Clerk Webhooks Endpoints > Signing Secret)`
- svix 설치
  - 엔드포인트 설정을 시작하려면 svix 패키지를 설치해야 합니다. 
  - Svix는 웹훅 서명을 확인하기 위한 패키지를 제공하므로 웹훅 이벤트의 진위 여부를 쉽게 확인할 수 있습니다.
- Webhook endpoint 만들기
  - app/api/webhook/route.ts 생성
    - svix 를 사용해서 웹훅 검증
    - eventType 별로 database 연동
      - create: 실제 로그인 후 DB 확인
      - update: 유저정보에서 유저명 변경 후 DB 확인
      - delete: 유저정보에서 계정 삭제 후 DB 확인
  - middleware.ts 수정
    ```ts
    export default authMiddleware({
      publicRoutes: ["/api/webhooks(.*)"]
    });
    ```
  - [Clerk 에서 웹훅 테스트하기](https://clerk.com/docs/users/sync-data#test-the-webhook)
    - Clerk > Webhooks > Endpoints > Testing 탭
      - Send event: user.created 선택 > Send Example
      - Send event: user.delete 선택 > Send Example

### dependencies
- `npm install svix`

### 참고
- [Sync Clerk data to your backend with webhooks](https://clerk.com/docs/users/sync-data#enable-webhooks)

## Navbar
- app/(browse) 생성
  - _component, (home) 폴더 생성 및 page 이동
- shadcn-ui input 라이브러리 추가
- query-string 라이브러리 추가
- middleware.ts 수정
  - publicRoutes 에 "/" 루트 추가
- app/(browse)/_components/navbar 추가
  - Navbar 컴포넌트 추가

### dependencies
- `npx shadcn-ui@latest add input`
- `npm i query-string`

## Sidebar
- app/(browse)/_components/sidebar 사이드바 관련 컴포넌트 추가
  - app/(browse)/_components/sidebar/index.tsx
  - app/(browse)/_components/sidebar/toggle.tsx
  - app/(browse)/_components/sidebar/wrapper.tsx
- store/use-sidebar.ts 생성
  - 사이드바 상태 훅
- app/(browse)/_components/container.tsx 생성

- components/hint.tsx 생성
  - 다른 컴포넌트의 hint 를 표시하는 컴포넌트
- app/(browse)/layout.tsx 수정
  - Sidebar, Container 컴포넌트 추가

### dependencies
- `npm i zustand`
  - 상태 관리 라이브러리
- `npx shadcn-ui@latest add tooltip`
- `npm i usehooks-ts`
  - 타입스크립트로 작성되어 바로 사용할 수 있는 React 후크 라이브러리

## Recommended list
- lib/auth-service.ts 생성
  - 인증 서비스
- lib/recommended-service.ts 생성
  - 추천 리스트에서 사용할 서비스
- app/(browse)/_components/sidebar/index.tsx 수정
  - Recommended 추가
- components/user-avatar.tsx 생성
  - 사용자 아바타 컴포넌트
- components/live-badge.tsx 추가
  - 라이브중인지 표시하기 위한 뱃지

### dependencies
- `npx shadcn-ui@latest add avatar`
- `npx shadcn-ui@latest add skeleton`

### Notes
**CVA(class-variance-authority)**
- CVA를 포함하면 사용자 친화적인 인터페이스를 마음대로 사용할 수 있어 이형 상품 정의를 간소화할 수 있습니다.
- 변형은 클래스 집합의 조건부 적용을 가능하게 하는 동시에 기본 변형을 표현할 수 있는 수단도 제공합니다.

## Hydration error
- app/(browse)/_components/sidebar/toggle.tsx 수정
  - 토클 스켈레톤 추가
- app/(browse)/_components/sidebar/index.tsx 수정
  - Recommended 스켈레톤 추가
- app/(browse)/_components/sidebar/wrapper.tsx 수정
  - Hydration 에러 방지
  - `useIsClient()` 를 사용

### Note
- 클라이언트 / 서버 사이드 렌더링에 따라 hydration 에러가 발생한다면 아래와 같이 예외처리를 할수 있습니다.
```ts
const [isClient, setIsClient] = useState(false);

useEffect(() => {
  setIsClient(true);
}, []);

if (!isClient) return (
  <aside
    className="fixed left-0 flex flex-col w-[70px] lg:w-60 h-full bg-background border-r border-[#2D2E35] z-50"
  >
    <ToggleSkeleton />
    <RecommendedSkeleton />
  </aside>
);
```
- usehooks-ts 를 사용하는 방법(useState 사용하지 않음)
```ts
const isClient = useIsClient();
.
.
```

## Follow service
- ngrok 으로 웹훅을 사용할수 있게 로컬 실행
- app/(browse)/[username]/page.tsx 생성
  - 유저 정보 페이지
- lib/user-service.ts 생성
  - DB 에서 유저명으로 유저정보 가져오기
- lib/follow-service.ts 생성
  - DB 에서 팔로우 유저 관련 정보
- app/layout.tsx 수정
  - sonner 토스트 추가
- actions/follow.ts 생성
  - 서버 사이드 렌더링
  - 유저정보 캐시
  - 팔로우 정보 가져오기
- app/(browse)/[username]/_components/actions.tsx 생성
  - 팔로우 버튼 및 액션

### dependencies
- `npm i sonner`
  - 토스트 라이브러리

## Follow list
- lib/follow-service.ts 수정
  - 팔로잉 리스트 가져오기
- app/(browse)/_components/sidebar/following.tsx 생성
  - 팔로잉 컴포넌트
- app/(browse)/_components/sidebar/index.tsx 수정
  - 팔로잉 컴포넌트 추가
  - 스켈레톤 추가
- app/(browse)/_components/sidebar/wrapper.tsx 수정
  - 스켈레톤 추가
- lib/recommended-service.ts 수정
  - 추천 리스트에서 팔로워 제거

## Block service
- prisma/schema.prisma 수정
  - Block 모델 추가
  - npx prisma generate
  - npx prisma db push
- lib/block-service.ts 생성
  - DB 유저 블록 정보 조회, 생성 및 삭제 기능 추가
- app/(browse)/[username]/page.tsx 수정
  - 사용자 정보 페이지 블록 정보 추가
- app/(browse)/[username]/_components/actions.tsx 수정
  - 블록 액션 추가
- lib/recommended-service.ts 수정
  - DB 조회시 블록 사용자 제외
- lib/follow-service.ts 수정
  - DB 조회시 블록 사용자 제외

## Creator dashboard
- app/(dashboard)/u/[username] 대시보드 관련 컴포넌트 생성
- lib/auth-service.ts 수정
  - 유저 이름 가져오기
- app/(dashboard)/u/[username]/layout.tsx 수정
  - 컨테이너 컴포넌트 추가
- app/(dashboard)/u/[username]/_components/container.tsx 생성
  - 컨텐트 영역 컨테이너 컴포넌트 추가
- store/use-creator-sidebar.ts 생성
  - sidebar 에서 사용할 상태 관리
- app/(dashboard)/u/[username]/_components/sidebar 컴포넌트 생성
  - app/(dashboard)/u/[username]/_components/sidebar/wrapper.tsx
    - 사이드바 전체를 감싸는 컴포넌트
  - app/(dashboard)/u/[username]/_components/sidebar/toggle.tsx
    - 사이드바 확장/비확장 컴포넌트
  - app/(dashboard)/u/[username]/_components/sidebar/navigation.tsx
    - 사이드바 네비게이션 컴포넌트
  - app/(dashboard)/u/[username]/_components/sidebar/nav-item.tsx
    - 사이드바 네비게이션 아이템 컴포넌트

## Stream model
- prisma/schema.prisma 수정
  - Stream 모델 추가
  - TextSearch 지원
    ```prisma
    generator client {
      provider = "prisma-client-js"
      previewFeatures = ["fullTextSearch", "fullTextIndex"]
    }
    ```
    - previewFeatures 추가
- `npx prisma migrate reset` 디비 초기화
- Clerk 유저 삭제 후 다시 생성
- 회원가입 후 stream 생성 되었는지 확인

### Node
[**Prisma Full-text search**](https://www.prisma.io/docs/orm/prisma-client/queries/full-text-search)
- Prisma 클라이언트는 버전 2.30.0 이상의 PostgreSQL 데이터베이스와 버전 3.8.0 이상의 MySQL 데이터베이스에 대한 전체 텍스트 검색을 지원합니다.
- 전체 텍스트 검색을 활성화하면 데이터베이스 열 내의 텍스트를 검색하여 애플리케이션에 검색 기능을 추가할 수 있습니다.
- MySQL의 경우 전체 텍스트 인덱스 미리 보기 기능 플래그도 포함해야 합니다:

예를 들어 다음 검색은 '고양이'라는 단어가 포함된 모든 게시물을 반환
```ts
// All posts that contain the word 'cat'.
const result = await prisma.posts.findMany({
  where: {
    body: {
      search: 'cat',
    },
  },
})
```

[**Prisma Full text indexes (MySQL and MongoDB)**](https://www.prisma.io/docs/orm/prisma-schema/data-model/indexes#full-text-indexes-mysql-and-mongodb)
- 전체 텍스트 인덱스 미리보기 기능은 버전 3.6.0 이상에서 MySQL 및 MongoDB의 전체 텍스트 인덱스에 대한 인스펙션 및 마이그레이션을 지원합니다. 
- 이 기능은 @@fulltext 속성을 사용하여 구성할 수 있습니다. 
- 데이터베이스의 기존 전체 텍스트 인덱스는 db pull으로 인트로스펙팅한 후 Prisma 스키마에 추가되며, Prisma 마이그레이션을 사용할 때 Prisma 스키마에 추가된 새 전체 텍스트 인덱스가 데이터베이스에 생성됩니다.
- 이렇게 하면 이전에 작동하지 않던 일부 데이터베이스 스키마의 유효성 검사 오류도 방지할 수 있습니다.

## Chat settings
- app/(dashboard)/u/[username]/chat/page.tsx 생성
  - 채팅 화면 구현
- lib/stream-service.ts 생성
  - Stream 서비스 user에 해당하는 stream 가져오기
- actions/stream.ts 생성
  - server 용 stream actions 생성
- shadcn-ui `switch` 추가
- components/ui/switch.tsx 수정
  - 스위치 색상 수정
- app/(dashboard)/u/[username]/chat/_components/toggle-card.tsx 생성
  - 스위치 카드 컴포넌트
- app/(dashboard)/u/[username]/chat/loading.tsx 생성
  - 페이지 로딩에 스켈레톤 표시

### dependencies
- `npx shadcn-ui@latest add switch`


# [Part 2](https://www.youtube.com/watch?v=nav55-4ISg4)
## Key settings
- app/(dashboard)/u/[username]/keys/page.tsx 생성
  - Keys 화면 생성
- app/(dashboard)/u/[username]/keys/_components/url-card.tsx 생성
  - URL 영역을 표시하는 컴포넌트
- app/(dashboard)/u/[username]/keys/_components/key-card.tsx 생성
  - 키 영역을 표시하는 컴포넌트
  - show/hide 에 따라서 Input 타입 변경(text/password)
- app/(dashboard)/u/[username]/keys/_components/copy-button.tsx 생성
  - 버튼 클릭시 값이 복사되는 컴포넌트
  - value 를 넘겨서 그 값을 복사
- app/(dashboard)/u/[username]/keys/_components/connect-modal.tsx 생성
  - 연결을 위한 다이얼로그 컴포넌트
  - dialog 안에서 select, alert 구현

### dependencies
- `npx shadcn-ui@latest add dialog`
- `npx shadcn-ui@latest add select`
- `npx shadcn-ui@latest add alert`

## Ingress
- actions/ingress.ts 생성
  - 서버에서 사용하는 액션 구현
- app/(dashboard)/u/[username]/keys/_components/connect-modal.tsx 수정
  - TRMP, WHIP 을 사용해서 서버 생성

### dependencies
- `npm i @livekit/componenets-react`
- `npm i livekit-client`
- `npm i livekit-server-sdk`

## OBS crash course
### [OBS Studio](https://obsproject.com/ko)
- 영상 녹화와 실시간 방송을 할 수 있는 무료 및 공개 소프트웨어입니다.

### OBS 스트리밍
1. 설정 > 방송
  - 서비스: 사용자 지정...
  - 서버: **스트림 서버 URL 입력**
  - 스트림 키: **스트림키 입력**
2. 방송 시작

### Livekit 네트워크 트래픽 확인
Egress/Ingress 탭 확인
- Egress: 서버 내부에서 외부로 나가는 트래픽을 의미
- Ingress: 외부로부터 서버 내부로 유입되는 네트워크 트래픽을 의미

스트리밍 후에 Ingresses에 항목이 추가됨

## Livekit webhook
- lib/recommended-service.ts 수정
  - include stream
- lib/follow-service.ts 수정
  - include stream
- app/(browse)/_components/sidebar/recommended.tsx 수정
  - isLive 속성 수정
- app/(browse)/_components/sidebar/following.tsx 수정
  - isLive 속성 수정
- LiveKit - 웹훅 EndPoint 추가
  - 대시보드 > Settings > WEBHOOKS > ADD NEW ENDPOINT
    - URL: https://national-utterly-beetle.ngrok-free.app/api/webhooks/livekit
    - API Key: **SIGNING API KEY**
- app/api/webhooks/livekit/route.ts 생성
  - 웹훅 API 추가
  - ingress 시작/종료시에 stream.isLive 상태 변경
- middleware.ts 확인
  - "/api/webhooks(.*)" 추가 되었는지 확인

## Viewer token
- lib/recommended-service.ts 수정
  - include stream 에 필요한 isLive 만 가져오도록 select 추가
- lib/follow-service.ts 수정
  - include stream 에 필요한 isLive 만 가져오도록 select 추가
- app/(browse)/_components/sidebar/following.tsx 수정
  - props Stream 대신 isLive 만 선언
- app/(browse)/_components/sidebar/recommended.tsx 수정
  - props Stream 대신 isLive 만 선언

### dependencies
- `npm i jwt-decode`
  - 이 라이브러리는 토큰의 유효성을 검사하지 않으며, 잘 형성된 JWT는 모두 디코딩할 수 있습니다. 
  - 서버 측 로직에서 express-jwt, koa-jwt, Microsoft.AspNetCore.Authentication.JwtBearer 등과 같은 것을 사용하여 토큰의 유효성을 검사해야 합니다.
- `npm i uuid`
  - uuid 가져오지 못하는 문제가 있어서  devDependencies 추가
  ```
  "devDependencies": {
      ...
      "@types/uuid": "^9.0.7",
    }"
  ```
- app/(dashboard)/u/[username]/(home)/page.tsx 수정
  - StreamPlayer 컴포넌트 추가
- actions/token.ts 생성
  - livekit 토큰을 사용해서 토큰 생성
- hooks/use-viewer-token.ts 생성
  - 토큰 생성을 요청
  - jwt-decode 를 통해서 토큰을 디코딩
  - 토큰 정보로 여러가지 기본 정보를 유지시켜주는 훅

## Video component
- next.config.js 수정
  - rule 추가
- components/stream-player 생성
  - stream 에 보여줄 컴포넌트 추가
    - index, video
- components/stream-player/live-video.tsx 생성
  - 비디오 컴포넌트 추가
  - 상태에 따라서 offline, loading, live 컴포넌트 교체
  - 컨트롤러 추가
    - fullscreen
    - volume
- components/stream-player/offline-video.tsx 생성
  - 비디오 오프라인 컴포넌트
- components/stream-player/loading-video.tsx 생성
  - 비디오 로딩 컴포넌트
- components/stream-player/fullscreen-control.tsx 생성
  - 비디오 풀 스크린 컴포넌트
- components/stream-player/volumn-control.tsx 생성
  - 볼륨 풀 스크린 컴포넌트

### dependencies
- `npx shadcn-ui@latest add slider`

### Note
**next.config.js 추가한 룰 분석**
```
webpack: (config) => {
    config.module.rules.push({
      test: /\.mjs$/,
      include: /node_modules/,
      type: "javascript/auto",
    });

    return config;
},
```
- test: 정규 표현식을 사용하여 파일 경로의 확장자가 .mjs로 끝나는지 확인합니다.
- include: 파일이 node_modules 디렉터리에 위치해야 합니다.
- type: 파일의 형식을 지정합니다. 여기서는 "javascript/auto"로 설정되어 있습니다.
즉, 이 규칙은 프로젝트의 node_modules 디렉터리에 속한 확장자가 .mjs인 파일들을 webpack이 자동으로 JavaScript 파일로 처리하도록 지시하는 것입니다.

## Chat component
- components/stream-player/index.tsx 수정
  - 채팅 사이드바 토글 추가
  - 채팅 컴포넌트 추가
- components/stream-player/chat.tsx 생성
  - 채팅 헤더 컴포넌트 추가 
  - 채팅 리스트 추가
  - 채팅 인풋 추가
- components/stream-player/chat-header.tsx 생성
  - 채팅 헤더 컴포넌트
- components/stream-player/chat-toggle.tsx 생성
  - 채팅 헤더 사이드바 토글 버튼
- components/stream-player/variant-toggle.tsx 생성
  - 채팅 헤더 채팅/커뮤니티 토글 버튼
- components/stream-player/chat-form.tsx 생성
  - 채팅 폼 컴포넌트
- components/stream-player/chat-info.tsx 생성
  - 채팅 폼 안의 정보 컴포넌트
- components/stream-player/chat-list.tsx 생성
  - 채팅 리스트 컴포넌트
- components/stream-player/chat-message.tsx 생성
  - 채팅 리스트 아이템 컴포넌트
  - date-fns 로 시간 포맷 구성
- store/use-chat-sidebar.ts 생성
  - 채팅에서 사용할 사이드바 훅
- lib/utils.ts 수정
  - string 으로 색상코드를 가져오는 유틸 추가

### dependencies 
- `npm i date-fns`

## Community component
- components/stream-player/chat-community.tsx 생성
- components/stream-player/community-item.tsx 생성
- components/stream-player/chat.tsx 수정
- components/stream-player/index.tsx 수정
  - 구현된 스켈레톤을 조합해서 표시
- components/stream-player/chat-header.tsx 수정
  - 헤더 스켈레톤 추가
- components/stream-player/video.tsx 수정
  - 비디오 스켈레톤 생성
- app/(dashboard)/u/[username]/(home)/loading.tsx 생성
  - 스트림 플레이어 스켈레톤 로딩 적용

### dependencies
- `npx shadcn-ui@latest add scroll-area`
  스크롤 영역 범위

## Header component
- components/stream-player/header.tsx 생성
  - 헤더 컴포넌트 생성
  - 스켈레톤 컴포넌트 추가
- components/stream-player/actions.tsx 생성
  - Follow/Unfollow 액션 추가
  - 스켈레톤 컴포넌트 추가
- components/stream-player/index.tsx 수정
  - 헤더 컴포넌트 추가
  - 스켈레톤 추가
- components/verified-mark.tsx 생성
  - 인증 마크 컴포넌트 생성

## Info card
## About card
## User page
## Home page
## Search page
## Unblock page
## Deployment
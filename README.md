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

## Stream model
## Chat settings

# [Part 2](https://www.youtube.com/watch?v=nav55-4ISg4)
## Key settings
## Ingress
## OBS crash course
## Livekit webhook
## Viewer token
## Video component
## Chat component
## Community component
## Header component
## Info card
## About card
## User page
## Home page
## Search page
## Unblock page
## Deployment
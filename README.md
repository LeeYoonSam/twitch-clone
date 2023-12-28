# Twitch Clone

Key Features:
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
  - .env 에 환경 변수 추가
    - 이 값은 사용자가 로그인하거나 가입할 때, 그리고 각 컴포넌트의 하단에 있는 각 링크를 클릭할 때 컴포넌트의 동작을 제어합니다.
- app/(auth)/layout.tsx 생성
  - Clerk UI Layout

### dependencies
- `npm install @clerk/nextjs`

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
## Clerk webhook
## Navbar
## Sidebar
## Recommended list
## Hydration error
## Follow service
## Follow list
## Block service
## Creator dashboard
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
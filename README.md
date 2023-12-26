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
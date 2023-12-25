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

## Routing concepts
## Authentication
## Dark mode
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
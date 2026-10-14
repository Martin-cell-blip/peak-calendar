# Peak Calendar 巅峰生理历

**An energy-aware calendar: it overlays a 24-hour energy curve on your schedule so demanding work lands where your energy actually is.**
把生理能量曲线叠在日程上，让高负荷任务落在真正有精力的时段。高保真可交互 Demo，一人完成（2025.09–2026.02），用 Google AI Studio、Gemini 和 Cursor 以 vibe-coding 方式迭代。

## Core features · 核心功能

- **Focus 能量日程** — an hourly schedule with a five-level energy colour overlay (低效 / 疲惫 / 平稳 / 高效 / 心流). Each event carries a 1–5 cognitive load; the app scores how well a task matches the energy of its slot and raises "智能平移 / 能量预警" coach insights.
- **Energy budget 精力余额** — every event consumes or restores energy by duration × intensity; the top-bar battery shows the projected end-of-day balance and shakes when the day is overbooked.
- **Flow Mode 心流模式** — a full-screen focus timer for one task; when the (simulated) heart rate crosses a threshold it opens a breathing prompt.
- **Pulse 能量预报** — a 24-hour energy area chart driven by a readiness state; a toggle switches between a rested day (85) and a low-readiness day (45) to show how the curve flattens.
- **Log 能量打卡** — drag to record how you feel right now; entries feed the analytics view.
- **Analytics 复盘** — weekly efficiency / sleep bars plus environment cards (weather, location) that illustrate how context could correlate with energy.
- **Zen 晚间回顾** — a quote card and an end-of-day wrap-up that classifies the day (Rest & Recovery / Balanced Flow / Peak Performance) from completed load.
- Light / dark theme; phone-frame layout centred on desktop.

**Scope note 边界说明**: this is a product prototype. Energy curves, HRV, heart rate, weather and location insights are **simulated in code** (`constants.ts`, `utils.ts`); there is no wearable or HealthKit integration yet, and no user data is collected. 这是产品原型：能量曲线、HRV、心率、天气与地点洞察都是代码里的模拟值，尚未接入任何可穿戴设备，也不收集用户数据。

## Tech stack · 技术栈

- React 19 + TypeScript 5.8, built with Vite 6
- Tailwind CSS, loaded via CDN in `index.html` with a small custom theme (glass colours, `float` / `pulse-slow` animations, class-based dark mode)
- `recharts` for the energy and analytics charts, `lucide-react` for icons
- No backend and no API keys required (the `GEMINI_API_KEY` entry in `vite.config.ts` is an AI Studio export default; the app does not call any model API)

```
App.tsx            view switch, readiness state, energy logs
types.ts           EnergyLevel, ScheduleEvent, Suggestion, CoachInsight …
constants.ts       mock schedule, weekly stats, environment insights
utils.ts           COLOR_SCALE, generateBioData, calculateMatchScore, calculateEnergyDelta
components/        AuraBackground · EnergyBattery · FlowMode · DailyWrapUp · MagSafeEffect · Layout
views/             FocusView · PulseView · LogEntryView · AnalyticsView · ZenView
```

## Run locally · 本地运行

Prerequisite: Node.js 18 or newer.

```bash
npm install
npm run dev        # http://localhost:3000
npm run build      # production build in dist/
npm run preview    # serve the build
```

Open the app, flip the readiness toggle on the **Pulse** tab, then return to **Focus** to watch the energy overlay and the battery react. The project also opens directly in Google AI Studio: https://ai.studio/apps/drive/1NlVzGvf67RtOHCFLaOUIeT-GY8utpt33

---

Author: Zhunming Ma 马准名 · Portfolio: https://zhunmingma-portfolio.vercel.app

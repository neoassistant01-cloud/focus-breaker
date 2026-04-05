# FocusBreaker - Specification

## Project Overview

- **Name:** FocusBreaker
- **Type:** Single-page micro-SaaS (HTML/CSS/JS)
- **Core functionality:** A focus timer that alerts users when their session ends, with daily streak tracking
- **Target users:** Productivity-focused individuals who want to avoid "rabbit-holing" during work sessions

---

## UI/UX Specification

### Layout Structure

- **Single page layout** - All content centered vertically and horizontally
- **Container:** Max-width 420px, centered
- **Sections (top to bottom):**
  1. App title/header
  2. Timer display (large, prominent)
  3. Duration selector (presets + custom)
  4. Control buttons (Start/Pause/Reset)
  5. Streak counter display
  6. Footer (subtle branding)

### Responsive Breakpoints

- **Mobile (< 480px):** Full-width, padding 16px, smaller font sizes
- **Desktop (≥ 480px):** Fixed max-width 420px, padding 24px

### Visual Design

#### Color Palette
- **Background:** `#0D111C` (deep dark blue-black)
- **Primary accent:** `#00E599` (mint green)
- **Secondary:** `#1A2332` (dark card background)
- **Text primary:** `#FFFFFF`
- **Text secondary:** `#6B7280`
- **Danger/Alert:** `#FF6B6B` (soft red for alerts)
- **Inactive/Disabled:** `#374151`

#### Typography
- **Font family:** "Outfit" from Google Fonts
- **Title:** 28px, weight 700
- **Timer display:** 72px, weight 300 (light)
- **Body text:** 16px, weight 400
- **Button text:** 16px, weight 600
- **Small text:** 14px, weight 400

#### Spacing System
- **Base unit:** 8px
- **Section gaps:** 32px
- **Element gaps:** 16px
- **Button padding:** 16px 32px
- **Card padding:** 24px
- **Border radius:** 12px (cards), 8px (buttons)

#### Visual Effects
- **Timer glow:** Subtle mint green text-shadow when running
- **Buttons:** Solid fill with slight scale on hover (1.02)
- **Alert animation:** Pulsing red glow when timer completes
- **Transitions:** All 0.2s ease

### Components

#### Timer Display
- Large MM:SS format (e.g., "25:00")
- Color: Mint green when running, white when paused/stopped
- Subtle pulsing glow animation while active

#### Duration Preset Buttons
- Presets: 25 min, 45 min, 60 min
- Pills/buttons in a row
- Active state: Mint green background
- Inactive: Dark background with border

#### Custom Duration Input
- Appears as a number input with "min" label
- Only visible when "Custom" is selected
- Range: 1-180 minutes

#### Control Buttons
- **Start:** Mint green, prominent
- **Pause:** Yellow/amber color (#F59E0B)
- **Reset:** Ghost/outline style
- States: Disabled when not applicable

#### Streak Counter
- Icon: Flame or target icon (SVG)
- Shows: "🔥 X sessions today"
- Updates in real-time after each completed session

#### Alert Overlay
- Full-screen semi-transparent overlay
- Red pulsing border
- "Time's Up!" message
- "Got it" button to dismiss

---

## Functionality Specification

### Core Features

1. **Timer Countdown**
   - Counts down from selected duration
   - Updates every second
   - Pausable and resumable
   - Resettable to selected duration

2. **Duration Selection**
   - Preset buttons: 25, 45, 60 minutes
   - Custom input field (1-180 min)
   - Changing duration resets timer to new value

3. **Completion Alert**
   - Play subtle audio chime (generated beep or from CDN)
   - Show visual overlay with "Time's Up!"
   - Increment streak counter
   - Auto-stop timer

4. **Streak Tracking**
   - Count completed sessions for current day
   - Store in localStorage with date key
   - Reset streak at midnight (check date on load)
   - Persist across page refreshes

5. **localStorage Persistence**
   - Key: `focusBreaker_data`
   - Store: `{ streak: number, lastDate: string }`
   - Update streak on session completion

### User Interactions

1. Select duration → Click preset or enter custom value
2. Start timer → Click Start button, timer begins
3. Pause timer → Click Pause, timer stops (can resume)
4. Reset timer → Click Reset, timer returns to selected duration
5. Complete session → Alert shows, user dismisses, streak increments

### Edge Cases

- Timer at 0:00 → Auto-complete, show alert
- Page refresh while running → Timer resets (no persistence of running state)
- Midnight rollover → Reset streak count
- Invalid custom input → Default to 25 min
- Audio blocked → Visual alert still works

---

## Acceptance Criteria

1. ✅ Timer displays in MM:SS format, counts down accurately
2. ✅ Preset buttons (25, 45, 60) work and highlight when selected
3. ✅ Custom duration input accepts 1-180 minutes
4. ✅ Start button begins countdown, changes to Pause when running
5. ✅ Pause button stops countdown, can resume with Start
6. ✅ Reset button returns timer to selected duration
7. ✅ At 0:00, alert overlay appears with sound
8. ✅ Streak counter increments after each completed session
9. ✅ Streak persists in localStorage and survives refresh
10. ✅ Streak resets on new day
11. ✅ Dark theme with mint green accent is applied
12. ✅ Outfit font loads from Google Fonts
13. ✅ Mobile responsive - works on 320px+ screens
14. ✅ No console errors on load or interaction

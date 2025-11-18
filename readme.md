# Trade With Her 💘📈

<img width="680" height="272" alt="image" src="https://github.com/user-attachments/assets/49a842cb-ab13-4c3e-8995-56aa837bf1e6" />


> A tiny 3D anime waifu that sits on your screen while you trade on Axiom / Photon and reacts in real time to your wins, losses, and degen moments.

**Wins make her happy. Losses make her sad.**  
She cheers, nags, celebrates, and occasionally bullies you into having risk management.

---

## ✨ What is this?

**Trade With Her** is a desktop companion app + overlay that:

- Shows a **3D anime waifu** on top of your trading screen (always-on-top, movable & resizable)
- Connects to **Axiom** and **Photon** (and optionally custom websockets / REST feeds)
- Reacts in real time to your **PNL, fills, liquidations, & orders**
- Plays **voice lines, sound effects, and animations** depending on how you’re trading
- Keeps basic **trading stats & mood history** so you can see how often you’re making her proud… or disappointed

This repo contains the **desktop app**, **overlay**, and **plugin system** for adding new waifus, voices, and behaviors.

---

## 🔧 Features

### 🎭 Emotional State Engine

Your waifu has a dynamic mood based on:

- **Recent PNL** (per trade + session)
- **Win rate over last X trades**
- **Max drawdown for the session**
- **Position size vs account size** (degen meter)
- **Time spent trading without a break**

She can be:

- `happy` – consistent wins, low tilt  
- `excited` – big wins, high volume  
- `worried` – overleveraged or revenge trading  
- `sad` – multiple losses in a row  
- `tsundere` – you’re up but trading like a maniac  
- `asleep` – idle for too long / markets quiet

These states control:

- Facial expressions
- Idle animations
- Voice line pools
- Special event triggers

---

### 📢 Reactive Voice Lines & SFX

Out of the box she reacts to:

- ✅ **Win:** “Nice one! That entry was clean~”
- ❌ **Loss:** “Oi. You promised to use a stop loss…”
- 💥 **Liquidation / huge loss:** dynamic “you okay?” / “touch grass” voice lines
- 📈 **New position opened**
- 📉 **Position closed**
- ⚠️ **Risk limit events** (size too big, too many trades, etc.)

Supports:

- Multiple **voice packs** (JP/EN, soft/tsun, etc.)
- **Randomized** lines so it doesn’t feel robotic
- Optional **cooldowns** (e.g. don’t spam 10 lines in 1s)
- Custom **sound sets** per strategy / account

---

### 🕹️ Screen Overlay & Controls

- Always-on-top 3D model that:
  - Can be **dragged** anywhere on screen  
  - Supports **scale** & **opacity** sliders  
  - Has **click interactions** (poke, headpats, high five)
- Optional **“Streamer Mode”** with:
  - No swear words
  - Minimal UI
  - Chat-friendly reactions

Hotkeys (fully configurable):

- `Ctrl+Shift+W` – toggle waifu visibility  
- `Ctrl+Shift+M` – mute / unmute sounds  
- `Ctrl+Shift+R` – reset position & scale  
- `Ctrl+Shift+P` – pause reactions (e.g. serious trading time)

---

### 📊 Trading Integrations

Currently “designed” to support:

- **Axiom**: via WebSocket / API key  
- **Photon**: via WebSocket / API key  
- **Custom feeds**:
  - Local HTTP endpoint
  - WebSocket with a simple trade event schema
  - Mock mode for demoing without real trades

Core events:

```ts
type TradeEvent = {
  platform: "axiom" | "photon" | "custom";
  side: "long" | "short";
  pnl: number;       // realized PNL
  unrealizedPnl: number;
  size: number;
  price: number;
  timestamp: number;
};

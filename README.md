# MeshWatch
We're building MeshWatch—an offline, Bluetooth-based micro-alert app for communities to quietly report immigration enforcement activity. No GPS, no cloud, no surveillance. Just encrypted messages relayed device-to-device. Join us.

# 🔵 MeshWatch

**MeshWatch** is an open-source, decentralized mobile app that allows users to **report and receive ICE (Immigration and Customs Enforcement) activity alerts via Bluetooth peer-to-peer communication**—no Wi-Fi, no cell service, no servers.

This tool is designed for at-risk communities who want to stay informed and safe without compromising privacy.

---

## 🚨 What Is It?

MeshWatch lets users broadcast short reports like:

- "2 black SUVs, 3 officers in vests – Toms River, Washington St."

These reports travel **via Bluetooth mesh networking**, hopping device to device. No GPS, no accounts, no logging. Think "offline Twitter" for spotting ICE, built to survive digital blackouts or surveillance threats.

---

## 🎯 Mission

Create a **privacy-first, offline-capable network** for local reporting of immigration enforcement presence—especially in immigrant and vulnerable communities—without depending on internet access or centralized platforms.

---

## ✨ Core Features (MVP)

- 📍 **Manual Location Input** (City + Street only)
- 📝 **Short Alert Messages** (280 characters max)
- 📡 **Bluetooth Mesh Messaging** (Nearby Connections API or Bridgefy)
- 📥 **Inbox of Nearby Reports** (local, cached, offline)
- 🧽 **Auto-delete Alerts** (after 24 hours)
- 🧘 **Anonymous & No Account Needed**

---

## 🔐 Privacy Principles

- **No GPS or geolocation used**
- **No names, emails, or phone numbers stored**
- **No cloud sync or backend database**
- **Optional panic-wipe mode** to erase all history instantly
- **All data stays local**, transmitted only via device-to-device Bluetooth

---

## 📱 Tech Stack (Android MVP)

| Component | Tech |
|----------|------|
| Platform | Android (Kotlin) |
| Networking | [Nearby Connections API](https://developers.google.com/nearby/connections/overview) or [Bridgefy SDK](https://bridgefy.me/) |
| UI | Jetpack Compose or XML |
| Storage | Room (temporary local DB) |
| Encryption | AES-256 local encryption (optional PGP layer later) |
| Map (future) | OpenStreetMap tiles or vector map overlay |

---

## 🛣 Roadmap

### ✅ Phase 1: MVP
- [x] Compose / XML UI for posting alerts
- [x] Bluetooth P2P communication
- [x] Local inbox
- [x] Expiration after 24 hours

### 🟡 Phase 2: Mesh Relay
- [ ] Relay messages over multiple devices
- [ ] Trust scoring for repeated/reliable nodes

### 🟢 Phase 3: Internet Bridge (optional)
- [ ] Post to public map if internet is available
- [ ] Email digest or Substack bridge

### 🟣 Phase 4: iOS Support
- [ ] Swift + MultipeerConnectivity port

---

## 🛠 Contributing

We’re looking for:

- Android developers (Kotlin / BLE experience a huge plus)
- UI/UX designers (simple + non-technical interface)
- Translators (Spanish, Haitian Creole, Tagalog, etc.)
- Security reviewers (local encryption / threat modeling)
- Community testers

Pull requests welcome. Open issues, fork the repo, and start building. Privacy is non-negotiable.

---

## 🌍 Who Is This For?

- Immigrant protection groups
- Community legal clinics
- Sanctuary churches
- Activists in blackout or no-signal regions
- Families trying to stay informed, quietly

---

## 📄 License

To be discussed: MIT, GPLv3, or AGPL (depending on contributor preference and deployment goals)

---

## 🤝 Code of Conduct

This project does not tolerate:
- Surveillance backdoors
- Abusive behavior toward contributors or users
- Commercialization of vulnerable user data

We stand with people—not platforms.

---

## 💡 Credits & Inspiration

- [Briar Project](https://briarproject.org/)
- [Bridgefy](https://bridgefy.me/)
- [FireChat](https://en.wikipedia.org/wiki/FireChat)
- Community alert networks in NJ and beyond

---

## 📬 Contact / Get Involved

Interested in contributing, piloting in your town, or sponsoring development?

Email: Sboege@gmail.com  
Or fork and start hacking.

We believe **safety starts with information—and that should never require a signal**.

<!-- Replace the placeholder image below with the real logo, e.g. ./profile/logo.png -->
<p align="center">
  <img src="https://placehold.co/160x160/png?text=Stokari+logo" alt="Stokari logo" width="140" height="140" />
</p>
<h1 align="center">📦 Stokari</h1>

<p align="center">
  Keep track of your shop's stock and sales, even when the internet isn't there.
</p>

<p align="center">
  <img alt="Status: early development" src="https://img.shields.io/badge/status-early%20development-orange" />
  <img alt="Offline first" src="https://img.shields.io/badge/offline-first-2ea44f" />
  <img alt="Installable PWA" src="https://img.shields.io/badge/app-installable%20PWA-5a0fc8" />
</p>

---

## 🛒 Why Stokari exists

Walk through a market like Merkato and you'll find most stock tracked in notebooks or Excel. Then the numbers drift. A sheet says 150 units, the shelf holds 63, and nobody knows where the other 87 went.

The apps that could fix this usually assume steady internet, a bigger budget, or a lot of training. Stokari is built around the opposite: a shop with a cheap Android phone, a patchy connection, and an owner who has never used inventory software.

> 🚧 **Early development.** The requirements (SRS v0.5) and system design (SDD v0.2) are written. Most of the code is not. Don't point a real shop at this yet.

## 📱 What you'll be able to do

- 🧾 Record a sale in a few taps, with or without a connection
- 📥 Log new stock when a delivery arrives
- 🕑 See the full history of any product: who changed it, when, and why
- 🔔 Get low-stock warnings and a simple summary of today's sales
- 👥 Invite attendants who can sell and receive stock, but can't see costs or change prices

It runs in the browser and installs to the home screen like an app. Target devices are low-end Android phones (Chrome) and desktop Chrome or Edge.

## 🔄 The tricky bit: two phones, one shelf

Stokari never stores stock as a number you can overwrite. Every sale, delivery, and correction is saved as its own permanent record, and a product's quantity is just the sum of those records. Cancelling a sale doesn't delete it; it adds a new record that puts the stock back.

This is what makes offline sync safe. Say a product has 10 units and two phones lose signal:

| Phone A sells | Phone B sells | What happens after sync |
|---|---|---|
| 2 | 3 | Both accepted. Stock is 5. |
| 7 | 6 | Together they sell more than the shop had. **Both sales are kept** and marked *Needs review*. The owner cancels one or corrects the count. |

A sale that happened at the counter shouldn't disappear because another phone reached the server first.

## 🧰 Built with

| Layer | Tools |
|---|---|
| 💻 Web app | Vite, React, TypeScript, Dexie (IndexedDB), TanStack Query |
| ⚙️ API | NestJS, Prisma, PostgreSQL |
| 🔐 Sign-in | Google (OpenID Connect) |
| ☁️ Hosting | Vercel, Render, Neon (free tiers) |

## 🗂️ Repositories

| Repo | Contents |
|---|---|
| [`web`](https://github.com/ORG_NAME/web) | The installable web app, local database, and sync client |
| [`backend`](https://github.com/ORG_NAME/backend) | The API, business rules, and database schema |

## 🗓️ Where we are

The plan is a four-week MVP, built in this order: products and single-device sales, then durable local records, then server storage with sign-in, then two-device sync and conflict handling, and finally staff permissions and testing on low-end phones. If time runs short, nice-to-haves like Amharic and the Ethiopian calendar go first.

## 🤝 Get involved

Found a bug or have an idea? Open an issue in the repo it belongs to. Setup steps live in each repo's own README.

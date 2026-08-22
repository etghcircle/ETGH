# 🗝️ The Memory Vault 💫

A living archive of **true friendship** ❤️ — where it all began, the moments that shaped it, and the memories three friends never want to lose.

Some stories are open for anyone to see 🌍. The rest stay just between us 🔐.

---

## 📖 What's Inside

- 📜 **Our Story** — how it all started, told the way we remember it.
- 🎬 **The Film** — an animated piece that captures the spirit of it.
- 📸 **Memories** — the moments, big and small, that we keep adding to.
- 🎲 **Fun Stuff** — inside jokes, random bits, things that just belong here.

Some of it is **public** 🌐 — anyone with the link can wander through it.
Some of it is **private** 🔒 — just for the three of us and Admin, locked behind a login.

## 👥 Who Can Do What

| 👤 Who | 👀 Can view | ✏️ Can add/edit |
|---|---|---|
| 🌍 Anyone (no login) | Public content only | Nothing |
| 🧑‍🤝‍🧑 Friend 1 / Friend 2 / Friend 3 | Everything | Only their own content |
| 👑 Admin | Everything | Everything |

🔑 Usernames are fixed — only passwords can be changed.

## ⚙️ Setup

```bash
# clone the repo
git clone <repo-url>
cd memory-vault

# Backend setup 🖥️
cd backend
./gradlew run

# Frontend setup 🎨 (in a new terminal)
cd frontend
./gradlew :frontend:kobwebStart
# Dev server runs at http://localhost:8080
```

You'll need:
- 🍃 **MongoDB** running locally (or set a remote connection string)
- ☁️ **Cloudinary** account for media hosting

Add your credentials to a local `.env` file (never commit this 🚫):

```
MONGODB_URI=mongodb://localhost:27017/memory-vault
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
JWT_SECRET=your_jwt_secret
```

## 📚 Project Docs

- 🏗️ `ARCHITECTURE.md` — folder layout and data flow
- 🧰 `TECH_STACK.md` — exact versions and approved/banned libraries
- 📝 `SRS.md` — full feature list and rules
- 💡 `DECISIONS.md` — why things are built the way they are

## 💌 A Note

This isn't a product. It's **three friends** 🫂 keeping their story somewhere safe 🗝️ — and letting a little of it out into the world 🌍.

**Three friends. One story. A lifetime of memories. ❤️✨**

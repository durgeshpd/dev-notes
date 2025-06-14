## ✅ Step-by-Step Git Workflow with Proper Commit Messages

1. 🧱 Initialize Git Repository

```bash
git init
```

---

2. 🚀 First Project Setup Commit
```bash
git add .
git commit -m "chore: initial project setup with Vite and folder structure"
```
---

3. ⚙️ Commit Project Config Files
```bash
git add .gitignore vite.config.js eslint.config.js
git commit -m "chore: add config files and ignore node_modules"
```
---

4. 📦 Commit Components (Individually or grouped logically)
```bash
# Navbar
git add src/components/Navbar.jsx
git commit -m "feat: add responsive Navbar component"

# Feed
git add src/components/Feed.jsx
git commit -m "feat: implement Feed component with posts display"

# Chat
git add src/components/Chat.jsx
git commit -m "feat: create Chat UI component"

# Login
git add src/components/Login.jsx
git commit -m "feat: build Login form with input validation"

# Connections + UserCard
git add src/components/Connections.jsx src/components/UserCard.jsx
git commit -m "feat: display connections using reusable UserCard"

# Edit Profile
git add src/components/EditProfile.jsx
git commit -m "feat: add EditProfile form layout"

# Profile
git add src/components/Profile.jsx
git commit -m "feat: show basic Profile information"

# Premium
git add src/components/Premium.jsx
git commit -m "feat: add Premium membership component with plans"
```
---

🕔 What If a Component Is Incomplete at Day-End?
Sometimes you start building a component (e.g. Premium.jsx), but don’t finish it before the day ends. Here’s what to do:

✅ Option 1: Save Work as WIP (Work in Progress)
```bash
git add src/components/Premium.jsx
git commit -m "wip: start building Premium component layout"
```
✅ Safe for local commits. Don’t push this to main.

✅ Option 2: Use a Feature Branch (Team-friendly)
```bash
git checkout -b feat/premium-component
git add src/components/Premium.jsx
git commit -m "wip: scaffold Premium component layout"
```
➡️ Later, when it's done:

```bash
git commit -m "feat: complete Premium component with UI and logic"
git checkout main
git merge feat/premium-component
```
✅ Option 3: Use Git Stash (No Commit)
```bash
git stash push -m "incomplete Premium component"
# Next time
git stash pop
```
🧠 Rule of Thumb: Always save your progress (via WIP, branch, or stash) — never leave work untracked overnight.

---

5. 🧠 Redux + Utilities
```bash
# Configure Redux Store
git add src/utils/appStore.js
git commit -m "feat: configure Redux store"

# Add user & feed reducers
git add src/utils/userSlice.js src/utils/feedSlice.js
git commit -m "feat: add user and feed reducers to Redux store"

# Add request & connection slices
git add src/utils/requestSlice.js src/utils/connectionSlice.js
git commit -m "feat: manage requests and connections using Redux slices"

# Add socket.io connection logic
git add src/utils/socket.js
git commit -m "feat: setup socket.io client for real-time communication"

# Define shared constants
git add src/utils/constants.js
git commit -m "chore: define global constants"
```
---

6. 🌐 Add App Entry & Routing
```bash
# Main app and entry point
git add src/main.jsx src/App.jsx
git commit -m "feat: setup main entry point and basic routing"

# Styling
git add src/style.css
git commit -m "style: add global styles"
```
---

7. ☁️ Push to GitHub
```bash
git remote add origin <your-repo-url>
git branch -M main
git push -u origin main
```
---

🧠 Smart Commit Message Patterns by Situation

---

## 🐛 Bug Fixes

| Scenario | Commit Message |
|----------|----------------|
| Button not clickable | `fix: make Submit button clickable after form validation` |
| API returning undefined | `fix: handle undefined API response in Feed` |
| Crash on null props | `fix: prevent crash when user data is null in Profile` |
| Redux not updating | `fix: update userSlice to correctly dispatch login action` |

---

## 🔐 Login & Authentication

| Scenario | Commit Message |
|----------|----------------|
| Create login form | `feat: design Login form UI with email/password fields` |
| Add validation | `feat: add form validation for login credentials` |
| Connect to backend | `feat: connect login form to authentication API` |
| Fix login issue | `fix: resolve issue where login fails with valid credentials` |
| Handle error UI | `feat: display login error messages from API` |

---

## 🖼️ UI & Layout Changes

| Scenario | Commit Message |
|----------|----------------|
| New layout | `feat: implement two-column layout for dashboard` |
| Style fix | `style: fix alignment of profile card` |
| Image/icon change | `chore: update app logo in Navbar` |
| Make responsive | `feat: make Feed component responsive on mobile` |
| CSS cleanup | `style: remove unused CSS classes in style.css` |

---

## ⚙️ Redux & State Management

| Scenario | Commit Message |
|----------|----------------|
| Add slice | `feat: add requestSlice for managing friend requests` |
| Configure store | `feat: configure Redux store` |
| Refactor logic | `refactor: simplify Redux store configuration` |
| Fix mutation bug | `fix: avoid direct mutation in feed reducer` |

---

## 🔌 API Integration

| Scenario | Commit Message |
|----------|----------------|
| Add new call | `feat: integrate /getConnections API with Connections.jsx` |
| Add loading state | `feat: show loading spinner while fetching posts` |
| Fix headers | `fix: correct request headers in login API call` |

---

## 🔄 Refactor & Cleanup

| Scenario | Commit Message |
|----------|----------------|
| Rename component | `refactor: rename UserCard to ProfileCard for clarity` |
| Remove console logs | `chore: remove debug logs from Chat component` |
| Extract logic | `refactor: extract fetchUser into custom hook` |

---

## 🌐 Routing

| Scenario | Commit Message |
|----------|----------------|
| Add routing | `feat: setup React Router and initial routes` |
| Add private routes | `feat: protect routes with authentication check` |
| Handle 404 | `fix: add catch-all route to redirect unknown paths` |

---

## 🔥 Real-Time Features

| Scenario | Commit Message |
|----------|----------------|
| Socket setup | `feat: setup socket connection in socket.js` |
| Chat handling | `feat: implement real-time messaging with sockets` |
| Fix socket issue | `fix: correct event listener for incoming messages` |

---

## 📁 Project Structure & Setup

| Scenario | Commit Message |
|----------|----------------|
| Initial setup | `chore: initial project setup with Vite and folder structure` |
| .env support | `chore: load environment variables from .env` |
| Git ignore | `chore: update .gitignore to exclude sensitive files` |

---

## 📄 Documentation

| Scenario | Commit Message |
|----------|----------------|
| Create README | `docs: add project README with setup instructions` |
| Add API docs | `docs: document available API endpoints` |
| Update instructions | `docs: update README with feature roadmap` |

---

## 🧪 Testing

| Scenario | Commit Message |
|----------|----------------|
| Add test | `test: add test for Navbar visibility logic` |
| Fix test | `fix: update test case for feed reducer` |
| Add test libs | `chore: install Jest and React Testing Library` |

---

## 🚀 Deployment

| Scenario | Commit Message |
|----------|----------------|
| Build config | `chore: add build script for Vite` |
| Hosting config | `chore: add config for Vercel deployment` |
| Prod bug | `fix: resolve build issue for production deployment` |

---

## ✅ Commit Types Reference

| Type       | Use For... |
|------------|------------|
| `feat`     | New features |
| `fix`      | Bug fixes |
| `style`    | CSS, formatting |
| `refactor` | Code improvement (no behavior change) |
| `chore`    | Config, setup, scripts |
| `docs`     | Documentation |
| `test`     | Tests |

---


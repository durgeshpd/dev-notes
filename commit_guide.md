## ✅ Step-by-Step Git Workflow with Proper Commit Messages

### 1. 🧱 Initialize Git Repository

```bash
git init
```
2. 🚀 First Project Setup Commit
```bash
git add .
git commit -m "chore: initial project setup with Vite and folder structure"
```
3. ⚙️ Commit Project Config Files
```bash
git add .gitignore vite.config.js eslint.config.js
git commit -m "chore: add config files and ignore node_modules"
```
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
git commit -m "feat: add placeholder Premium section"
```
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
6. 🌐 Add App Entry & Routing
```bash
# Main app and entry point
git add src/main.jsx src/App.jsx
git commit -m "feat: setup main entry point and basic routing"

# Styling
git add src/style.css
git commit -m "style: add global styles"
```
7. ☁️ Push to GitHub
```bash
git remote add origin <your-repo-url>
git branch -M main
git push -u origin main
```

🧠 Smart Commit Message Patterns by Situation
🔐 Login & Auth
Situation	Commit Message
Form + validation	feat: build Login form with input validation
Auth integration	feat: connect login form to authentication API
Handle errors	feat: display login error messages from API
Fix login bug	fix: resolve issue where login fails with valid credentials

🖼️ UI & Layout
Situation	Commit Message
New layout	feat: implement two-column layout for dashboard
Style fix	style: fix alignment of profile card
Mobile view	feat: make Feed component responsive on mobile

⚙️ Redux State
Situation	Commit Message
Create slice	feat: add requestSlice for managing friend requests
Update reducer	fix: correct state mutation bug in userSlice

🐞 Bug Fixes
Situation	Commit Message
Crash on null	fix: prevent crash when user data is null in Profile
API issue	fix: handle undefined API response in Feed.jsx

🔌 API & Backend
Situation	Commit Message
Fetch data	feat: integrate /getConnections API with Connections.jsx
Loading UI	feat: show spinner while fetching posts

📁 File Structure
Situation	Commit Message
Folder setup	chore: initial project structure with components and utils
Add config	chore: add environment config files

📄 Documentation
Situation	Commit Message
Create README	docs: add README with setup and usage
Add API info	docs: document authentication and feed APIs

✅ Git Commit Type Reference
Type	Use For...
feat:	New features
fix:	Bug fixes
style:	CSS/formatting only
refactor:	Code restructure (no logic change)
chore:	Setup, config, maintenance
docs:	Documentation
test:	Testing-related

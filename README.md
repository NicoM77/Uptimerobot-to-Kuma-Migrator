# 🛠️ UptimeRobot to UptimeKuma Migration Tool (Enhanced Edition)

This tool helps you migrate your monitors from **UptimeRobot** to **UptimeKuma**
with ease.

It is based on the original project
[sandstorm/uptime-robot-to-kuma-helper](https://github.com/sandstorm/uptime-robot-to-kuma-helper),
but has been **extended, modernized, and updated** for current environments.

---

## 🚀 What's New in This Version?

- ✅ Updated dependencies and compatibility with the latest Node.js & UptimeKuma
  versions.
- 🧹 Added command to **delete all monitors from UptimeKuma** (helpful for
  repeated tests or fresh migrations):

  ```bash
  yarn delete-kuma
  ```

  ⚠️ **Warning:** This will permanently remove all monitors from your Kuma
  instance.

---

## 🧩 How to Use

### 1. Prepare your Environment

Copy the sample environment file:

```bash
cp .env.sample .env
```

Then, edit `.env` to include your **UptimeRobot API Key** and **UptimeKuma
credentials**.

---

### 2. Start a Local UptimeKuma (for testing)

```bash
docker run --rm -p 3001:3001 --name uptime-kuma louislam/uptime-kuma:1
```

Once it’s running, complete the initial setup at
[localhost:3001](http://localhost:3001) and ensure login details match those in
your `.env`.

---

### 3. Run the Migration

```bash
# Step 1: Import your UptimeRobot monitors into UptimeKuma
yarn copy-monitors

# Step 2: Disable all UptimeRobot monitors
yarn disable-uptime-robot

# Step 3: (Danger Zone) Delete all UptimeRobot monitors
yarn delete-uptime-robot

# Step 4: (NEW) Delete all UptimeKuma monitors
yarn delete-kuma
```

---

## ⚙️ Architecture Overview

### 🟢 UptimeRobot: Easy Export

UptimeRobot offers a well-documented REST API, which makes fetching monitors
straightforward.

### 🔴 UptimeKuma: UI Automation

UptimeKuma does **not** (yet) offer a public API to create monitors. Originally,
the script used WebSocket injection—this proved unstable and unreliable.

To solve this, we now use **[Playwright](https://playwright.dev/)** to automate
a real browser session. This ensures consistent monitor creation via the actual
UptimeKuma UI.

---

## ⚠️ Limitations

- This tool was created for specific internal use cases and **may not cover 100%
  of UptimeRobot features**.
- Use with caution and test thoroughly before applying to production
  environments.

---

## 💡 Pro Tips

- Create a **default notification channel** in UptimeKuma _before_ migration. It
  will be automatically assigned to all imported monitors.
- Backup your UptimeKuma database before performing destructive operations.

---

## 🤝 Credits

Based on:
[sandstorm/uptime-robot-to-kuma-helper](https://github.com/sandstorm/uptime-robot-to-kuma-helper)
Extended & Updated by: \[Your Name or Team Name]

# Get Bot Token and Pairing with OpenClaw

> This guide covers how to get a bot token and complete pairing to connect a chat channel with OpenClaw on AgentBase.
> If you haven't deployed OpenClaw yet, see: [Deploy & Manage OpenClaw](deploy-and-manage-openclaw.md).

## Part 1 — Get a Bot Token from Telegram

### Step 1: Create a new bot on BotFather

1. Open Telegram and search for **@BotFather** (official blue checkmark).
2. Send the command `/newbot`.
3. Enter a **display name** for your bot (e.g. `My OpenClaw Bot`).
4. Enter a **username** — must end with `bot` (e.g. `my_openclaw_bot`).

### Step 2: Copy the Bot Token

After creation, BotFather returns a message containing a token in this format:

```
1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
```

Copy this token and store it somewhere safe — you will need it when configuring the Telegram channel in AgentBase.

> **Note:** The token is a secret — do not share it publicly.

---

## Part 2 — Pair your Telegram account with OpenClaw

### Step 1: Get the Pairing Code

1. Open Telegram and find the bot you just created (e.g. `@my_openclaw_bot`).
2. Tap **Start** or send `/start`.
3. The bot replies with a **pairing code**, for example:

```
Your pairing code is: ABC123DEF456

Please run this command in OpenClaw:
openclaw pairing approve telegram ABC123DEF456
```

### Step 2: Approve Pairing in OpenClaw Gateway

Go to **OpenClaw Gateway Dashboard** → find the chat box and enter:

```
openclaw pairing approve telegram <pairing_code>
```

Replace `<pairing_code>` with the code from Step 1.

### Result

- Pairing successful → the bot starts receiving and replying to your messages on Telegram.
- If the code expires → send `/start` again on Telegram to get a new code.

---

## Part 3 — Get a Bot Token from Zalo

> **Note:** The Zalo channel is currently **Experimental**. Direct Messages (DM) are fully supported; group and media features may be unstable.

### Step 1: Create a bot on Zalo Platform

1. Go to [https://bot.zaloplatforms.com](https://bot.zaloplatforms.com) and log in with your Zalo account.
2. Create a new bot, set a name (e.g. `Hana OpenClaw Bot`), and fill in the basic info.
3. Once created, open **bot settings** and copy the **Bot Token**.

### Step 2: Copy the Bot Token

Zalo tokens follow the format `numeric_id:secret`, for example:

```
1234567890123456789:abcXYZexampleTokenSecretKey123
```

Copy the **full token** (including everything after the `:`).

> **Note:** Zalo tokens are longer than Telegram tokens — make sure you copy the complete `:secret` part.

---

## Part 4 — Pair your Zalo account with OpenClaw

### Step 1: Get the Pairing Code

1. Open Zalo and send a message to the bot you just created.
2. Send `/start` or `Hello`.
3. The bot replies with an 8-character **pairing code** (e.g. `EXMP1234`). The code is valid for **1 hour**.

### Step 2: Approve Pairing in OpenClaw Gateway

Go to **OpenClaw Gateway Dashboard** → find the chat box and enter:

```
openclaw pairing approve zalo <pairing_code>
```

Replace `<pairing_code>` with the code from Step 1.

### Result

- Pairing successful → the bot starts receiving and replying to your messages on Zalo.
- If the code expires → send `/start` again on Zalo to get a new code.

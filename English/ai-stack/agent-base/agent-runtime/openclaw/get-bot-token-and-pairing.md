# Get Bot Token and Pairing with OpenClaw

> This guide covers how to get a bot token and complete pairing to connect a chat channel with OpenClaw on AgentBase.
> If you haven't deployed OpenClaw yet, see: [Deploy & Manage OpenClaw](deploy-and-manage-openclaw.md).

{% hint style="warning" %}
**Get your bot token before you deploy.** The **Bot Token** field in the **Channel Configuration** step is optional, but you should fill it in there. If you leave it empty and only add the token after the instance exists, you have to ask the agent inside OpenClaw to update the channel configuration itself — which is hard to do and easy to get wrong. Do **Part 1** (Telegram) or **Part 3** (Zalo) first, then paste the token into the deploy form.
{% endhint %}

{% hint style="warning" %}
**Only pair once the instance is Active.** Pairing requires a running OpenClaw instance. Open **My Agents** and confirm the status is 🟢 **Active** before sending `/start` to your bot.
{% endhint %}

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

Copy this token and store it somewhere safe — you will paste it into the **Bot Token** field in the **Channel Configuration** step when you [deploy OpenClaw](deploy-and-manage-openclaw.md).

> **Note:** The token is a secret — do not share it publicly.

---

## Part 2 — Pair your Telegram account with OpenClaw

### Step 1: Get the Pairing Code

Confirm your OpenClaw instance is 🟢 **Active** in **My Agents** before doing this step.

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

Copy the **full token** (including everything after the `:`) and paste it into the **Bot Token** field in the **Channel Configuration** step when you [deploy OpenClaw](deploy-and-manage-openclaw.md).

> **Note:** Zalo tokens are longer than Telegram tokens — make sure you copy the complete `:secret` part.

---

## Part 4 — Pair your Zalo account with OpenClaw

### Step 1: Confirm the OpenClaw instance is Active

Open **My Agents** and check that the instance status is 🟢 **Active**.

{% hint style="warning" %}
**Do not send `/start` while the instance is still `Creating`.** The Zalo bot can only generate a pairing code once the OpenClaw instance is running. If you message `/start` while the instance is still being created, the bot returns **no pairing code at all** — and that message is not reprocessed once the instance becomes Active. Wait until the status is **Active**, then send `/start`.
{% endhint %}

### Step 2: Get the Pairing Code

1. Open Zalo and send a message to the bot you just created.
2. Send `/start` or `Hello`.
3. The bot replies with an 8-character **pairing code** (e.g. `EXMP1234`). The code is valid for **1 hour**.

### Step 3: Approve Pairing in OpenClaw Gateway

Go to **OpenClaw Gateway Dashboard** → find the chat box and enter:

```
openclaw pairing approve zalo <pairing_code>
```

Replace `<pairing_code>` with the code from Step 2.

### Result

- Pairing successful → the bot starts receiving and replying to your messages on Zalo.
- If the code expires → send `/start` again on Zalo to get a new code.
- If the bot returns **no code at all** → the instance isn't Active yet, or the channel has no Bot Token. Check the instance status in **My Agents** and the channel configuration at **Settings → Config**, then send `/start` again.

# Limitations & Notes

## Current Limitations

| Limitation | Description |
| --- | --- |
| **Custom domain** | Not supported |
| **Team/shared instance** | Not supported |
| **Data backup** | Not supported |
| **Deploy Node from Gateway** | Not supported (Coming Soon — Phase 2) |

***

## Important Notes

{% hint style="warning" %}
**Deletion is permanent:**

When you delete an instance, all associated data is **permanently deleted** and cannot be recovered. Make sure you have backed up any necessary data before proceeding.
{% endhint %}

{% hint style="warning" %}
**BYOK — Invalid API key:**

If a BYOK API key expires or is revoked after deployment, the instance will no longer be able to call the AI model. Update the key at **Settings → Config** in the OpenClaw Gateway.
{% endhint %}

***

## Channel connection notes

| Situation | Why it matters | What to do |
| --- | --- | --- |
| **Bot Token left empty at deploy** | The deploy form doesn't require a Bot Token, but adding one after the instance is created means asking the agent to update the channel configuration itself — hard to do and easy to get wrong | Get the bot token first, then enter it in the **Channel Configuration** step while deploying |
| **Sending `/start` while the instance is `Creating`** | The bot can only generate a pairing code once the instance is running; send too early and the bot returns **no code at all**, and that message is not reprocessed once the instance becomes Active | Wait for 🟢 **Active** in **My Agents**, then send `/start` |

Details: [Get Bot Token and Pairing](get-bot-token-and-pairing.md).

***

If you encounter any difficulties, please contact the GreenNode team for support.

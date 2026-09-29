# AI Supply Chain Control Tower

A multi-agent supply chain monitoring workflow built in **n8n**. Three specialist AI agents analyse the supply chain, an orchestrator resolves conflicts between them, and a human approves the final recommendations on **Discord**.

## How it works

1. **Delay Agent**: flags delayed shipments and orders at risk.
2. **Cost Agent**: evaluates the cost impact of possible fixes.
3. **Inventory Agent**: checks stock levels and stockout risk.
4. **Orchestrator (Groq LLM)**: merges the three reports, resolves conflicts (e.g. air freight fixes delay but hurts cost) and returns 3 to 5 prioritised recommendations (P1/P2/P3) with cost impact and affected orders/SKUs.
5. **Human approval (Discord)**: the recommendation is posted to a Discord channel with Approve / Reject buttons.
6. **Notification**: the result (approved or rejected) is posted back to the same channel.

No Google Sheets or other external data source is required.

## Tech stack

- n8n (workflow automation)
- Groq API (OpenAI-compatible LLM endpoint)
- Discord bot (approval and notifications)

## Setup

1. Import `workflows/control-tower.json` into n8n (**Workflows > Import from file**).
2. Open the **CONFIG** node and fill in:
   - `groq_api_key`: your key from console.groq.com
   - `groq_model`: the Groq model you want to use
   - `discord_guild_id`: your Discord server ID
   - `discord_channel_id`: the channel for approvals
3. Create a Discord bot, invite it to your server, then add a **Discord Bot account** credential in n8n.
4. Click **Execute Workflow**, then approve or reject in Discord.

> Never commit real API keys or tokens. See `.env.example` for the list of values you need.

## Project structure

```
workflows/   n8n workflow JSON
data/        sample / dummy data
docs/        screenshots and diagrams
```

## License

MIT

# 🌐 OpenUSDT — The Open Source USDT Payment Gateway

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Build](https://img.shields.io/github/actions/workflow/status/openusdt/openusdt/ci.yml?label=build)](https://github.com/openusdt/openusdt/actions)
[![npm](https://img.shields.io/npm/v/@openusdt/sdk)](https://www.npmjs.com/package/@openusdt/sdk)
[![Discord](https://img.shields.io/discord/1234567890?logo=discord&label=community)](https://discord.gg/openusdt)
[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](#-contributing)

> **Stripe did it for credit cards.**  
> **We’re doing it for USDT.**  
> 100% open-source. No fees. Vibecoder-friendly.

---

## ✨ What is OpenUSDT?

OpenUSDT is an **open-source, developer-first payment gateway for USDT** across multiple blockchains (TRON, Ethereum, Polygon, Solana).  
It’s designed to be **prompt-friendly for Lovable.dev**, simple for *vibecoders*, and powerful enough for production apps.

✅ Accept USDT in minutes  
✅ No middlemen, no fees — just network gas  
✅ Lovable.dev integration (prompt recipes)  
✅ Supabase edge-function templates  
✅ React widgets + npm SDK  
✅ Sandbox simulator for testing  
✅ Webhook events (Stripe-style)

---

## 🛠️ Tech Stack

- **Core API** — Hono/Fastify (runs anywhere: Node, Edge, Workers)  
- **Chains** — TRON (TRC-20), Ethereum/Polygon (ERC-20), Solana (SPL)  
- **Storage/DB** — Supabase (optional templates)  
- **SDK** — `@openusdt/sdk` (JavaScript/TypeScript)  
- **UI** — `@openusdt/widgets` (React drop-ins)  
- **MCP Tool** — for AI agents & vibe coding  
- **CLI** — `openusdt` for init/dev/simulate  

---

## ⚡ Quickstart

### 1. Install SDK
```bash
npm install @openusdt/sdk @openusdt/widgets
2. Create a Payment Intent
ts
Copy code
import { OpenUSDT } from "@openusdt/sdk";

const client = new OpenUSDT({ baseUrl: "http://localhost:8787" });

const pi = await client.createPaymentIntent({
  amountUsd: 19.99,
  network: "tron",
  metadata: { orderId: "ORD-42" }
});

console.log(pi.depositAddress, pi.qr);
3. Embed Checkout Widget
tsx
Copy code
import { USDTCheckout } from "@openusdt/widgets";

<USDTCheckout amountUsd={19.99} network="tron" onSuccess={(pi) => {
  alert("Payment confirmed!");
}} />
4. Handle Webhook (Supabase Edge Function example)
ts
Copy code
import { verify } from "@openusdt/verifier";

export default async function handler(req) {
  const sig = req.headers["openusdt-signature"];
  const event = verify(req.rawBody, sig, process.env.OPENUSDT_WH_SECRET);

  if (event.type === "payment_intent.succeeded") {
    // Mark order as paid ✅
  }
  return { status: 200 };
}
🧑‍💻 Lovable Prompt Recipes
Paste these directly into Lovable.dev

Basic Checkout
“Install @openusdt/sdk and @openusdt/widgets. Add a /checkout page with <USDTCheckout amountUsd={19.99} network='tron' />. Configure webhook /api/openusdt_webhook to mark orders as paid in Supabase.”

Admin Payments Page
“Create an admin route /admin/payments that lists all confirmed payments from Supabase payments table, with filters for network and status.”

📦 Packages
@openusdt/sdk → JavaScript/TypeScript client

@openusdt/widgets → React checkout/drop-in components

@openusdt/verifier → Webhook signature verification

openusdt/cli → CLI for sandbox, simulate txs, init projects

openusdt/mcp → Model Context Protocol tool for AI integration

📊 Roadmap
 MVP: TRON + Ethereum support, static addresses, widget, Supabase example

 Derived addresses (HD wallets, sweeper)

 Polygon + Solana support

 Refunds, under/overpay handling

 Hosted checkout links

 Payouts (merchant disbursements)

 KYT hooks + compliance modules

👉 Check the Issues for what’s next!

🤝 Contributing
We welcome PRs, issues, and ideas!
See CONTRIBUTING.md for guidelines.

Fork the repo

Create your feature branch (git checkout -b feature/awesome)

Commit changes (git commit -m 'Add some awesome')

Push (git push origin feature/awesome)

Open a PR 🎉

🛡️ Security
Webhook signatures (HMAC w/ timestamp)

Configurable confirmations per network

Non-custodial by default

Custody mode optional (merchant-side only)

See SECURITY.md for reporting vulnerabilities.

📜 License
Apache 2.0 — free for personal and commercial use.
See LICENSE for details.

🌍 Join the Community
💬 Discord

🐦 Twitter

📖 Docs

Made with ❤️ for builders, vibecoders & dreamers.
Accept USDT anywhere, in minutes.

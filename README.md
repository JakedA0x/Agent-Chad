# Agent Chad

Agent Chad is a lightweight AI agent built on Cloudflare Workers. It provides a simple chat interface with Gemini-powered responses and persistent conversation memory using Cloudflare D1.

The project is designed as a minimal foundation that can be extended with web search, external tools, document retrieval, market data, and other agent capabilities.

## Features

* Cloudflare Workers backend
* Gemini API integration
* Cloudflare D1 conversation storage
* Browser-based session management
* Responsive web interface
* Server-side API key storage
* Deployable to `*.workers.dev`
* No VPS or traditional server required

## Architecture

```text
Browser
   │
   ▼
Cloudflare Worker
   │
   ├── Gemini API
   │
   └── Cloudflare D1
          │
          └── Conversation Memory
```

## Requirements

* Node.js
* A Cloudflare account
* A Gemini API key
* Wrangler CLI

## Installation

Clone the repository and install the dependencies:

```bash
npm install
```

Authenticate Wrangler with your Cloudflare account:

```bash
npx wrangler login
```

## Configure D1

Create a D1 database:

```bash
npx wrangler d1 create ai-agent-db
```

Cloudflare will return a `database_id`. Add that ID to `wrangler.toml`.

Example:

```toml
[[d1_databases]]
binding = "DB"
database_name = "ai-agent-db"
database_id = "YOUR_DATABASE_ID"
```

## Initialize the Database

Apply the database schema to the remote D1 database:

```bash
npx wrangler d1 execute ai-agent-db --remote --file=schema.sql
```

## Configure Gemini

Store the Gemini API key as a Cloudflare Worker secret:

```bash
npx wrangler secret put GEMINI_API_KEY
```

Enter the API key when prompted.

The key is stored on the server and is not exposed to the browser.

## Deploy

Deploy the Worker:

```bash
npx wrangler deploy
```

After deployment, Wrangler will provide the Worker URL:

```text
https://agent-chad.<subdomain>.workers.dev
```

## Health Check

The project includes a basic health endpoint.

Open:

```text
https://YOUR-WORKER.workers.dev/api/health
```

A successful deployment should return:

```json
{
  "ok": true
}
```

## Project Structure

```text
agent-chad/
├── src/
│   └── index.js
├── schema.sql
├── wrangler.toml
├── package.json
└── README.md
```

## Configuration

The main configuration is handled through `wrangler.toml`.

Sensitive values such as the Gemini API key should be stored using Cloudflare Worker secrets rather than committed to the repository.

Do not commit `.env` files, API keys, or other credentials.

## Development

For local development:

```bash
npx wrangler dev
```

Wrangler will start a local development server and provide a local URL.

## Roadmap

The initial version focuses on the core agent and conversation memory.

Potential future additions include:

* Web search
* URL and webpage reading
* Document and PDF processing
* R2 file storage
* Long-term memory
* Tool calling
* Crypto market data
* On-chain data
* News research
* Streaming responses
* Authentication
* Multi-agent workflows
* Research dashboard

## License

This project is currently provided as an open-source experiment. A formal license can be added when the project reaches a stable release.

# Free AI Agent V1 — Cloudflare

## Fitur
- Web UI
- Cloudflare Worker
- Cloudflare D1 conversation memory
- Gemini API
- Session ID di browser
- Responsive
- Deploy dengan `*.workers.dev`

## 1. Install
```bash
npm install
```

Login:
```bash
npx wrangler login
```

## 2. Buat D1
```bash
npx wrangler d1 create ai-agent-db
```

Salin `database_id` ke `wrangler.toml`.

## 3. Buat tabel
```bash
npx wrangler d1 execute ai-agent-db --remote --file=schema.sql
```

## 4. Pasang API key sebagai secret
```bash
npx wrangler secret put GEMINI_API_KEY
```

Masukkan API key saat diminta. Jangan pernah menaruh API key di frontend.

## 5. Deploy
```bash
npx wrangler deploy
```

Cloudflare akan memberikan URL:
`https://free-ai-agent-v1.<subdomain>.workers.dev`

## 6. Test
Buka:
`https://YOUR-WORKER.workers.dev/api/health`

Jika:
```json
{"ok":true}
```
berarti backend hidup.

## Catatan
Free tier/provider limits dapat berubah. V1 sengaja tidak memakai web search agar benar-benar sederhana dan murah. Tool web search, file upload/R2, auth, streaming, dan multi-agent dapat ditambahkan di V2.

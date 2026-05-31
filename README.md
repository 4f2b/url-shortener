# url-shortener-api

url shortener. send a long url, get a short one back. that's it.

postgres + express + node. docker included so you don't have to fight with setup.

> made by andrew / 9joe on discord

---

## features

- shorten urls
- redirect on hit
- custom slugs if you want
- expiry dates
- click tracking
- rate limiting so randoms don't spam it

---

## run it

the easy way:

```bash
git clone https://github.com/yourname/url-shortener-api
cd url-shortener-api
cp .env.example .env
docker compose up
```

without docker:

```bash
npm install
psql -U youruser -d yourdb -f db/migrations/001_create_urls.sql
npm run dev
```

---

## env

```env
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/urlshortener
BASE_URL=http://localhost:3000
```

---

## endpoints

**POST /api/shorten**

```json
{
  "url": "https://whatever.com/very/long/url",
  "slug": "mylink",
  "expiresAt": "2025-12-31T00:00:00.000Z"
}
```

slug and expiresAt are optional.

```json
{
  "success": true,
  "data": {
    "shortUrl": "http://localhost:3000/mylink",
    "code": "mylink",
    "originalUrl": "https://whatever.com/very/long/url"
  }
}
```

**GET /:code**

redirects. 404 if expired or doesn't exist.

**GET /api/stats/:code**

```json
{
  "success": true,
  "data": {
    "code": "mylink",
    "clicks": 42,
    "createdAt": "2024-01-01T00:00:00.000Z"
  }
}
```

---

## tests

```bash
npm test
```

---

## contributing

open an issue before a big pr. for small stuff just send it.

---

mit license

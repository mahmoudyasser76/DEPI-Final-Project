# URL Shortener

A simple, fast URL shortener built with Node.js, SQLite, and vanilla JavaScript.

## Features

- 🚀 Fast URL shortening with unique 7-character codes
- 📊 Analytics tracking (access count, timestamps, user agent, IP)
- 🎨 Modern dark theme UI with glassmorphism effects
- 🐳 Docker support for easy deployment
- 📈 Prometheus metrics

## Quick Start

### Local Development

1. **Install dependencies:**

   ```bash
   npm install
   ```

2. **Start the server:**

   ```bash
   npm start
   ```

3. **Open in browser:**
   ```
   http://localhost:2020
   ```

### Docker Deployment

1. **Using Docker Compose (Recommended):**

   ```bash
   docker-compose up -d
   ```

2. **Using Docker directly:**
   ```bash
   docker pull mahmoudyasser76/url-shortener:latest
   docker run -d -p 2020:2020 -v $(pwd)/data:/app/data mahmoudyasser76/url-shortener:latest
   ```

See [DOCKER_GUIDE.md](DOCKER_GUIDE.md) for detailed Docker instructions.

## API Endpoints

### POST /api/shorten

Shorten a URL.

**Request:**

```json
{
  "url": "https://example.com/very/long/path"
}
```

**Response:**

```json
{
  "shortUrl": "http://localhost:2020/abc123",
  "shortCode": "abc123",
  "originalUrl": "https://example.com/very/long/path"
}
```

### GET /:shortCode

Redirects to the original URL and logs analytics.

### GET /api/stats/:shortCode

Get statistics for a shortened URL.

**Response:**

```json
{
  "short_code": "abc123",
  "original_url": "https://example.com/very/long/path",
  "created_at": "2025-11-27 01:09:58",
  "access_count": 42,
  "last_accessed_at": "2025-11-27 03:45:12"
}
```

## Database Schema

### urls table

| Column           | Type     | Description           |
| ---------------- | -------- | --------------------- |
| id               | INTEGER  | Primary key           |
| short_code       | TEXT     | Unique short code     |
| original_url     | TEXT     | Original long URL     |
| created_at       | DATETIME | Creation timestamp    |
| access_count     | INTEGER  | Number of accesses    |
| last_accessed_at | DATETIME | Last access timestamp |

### url_analytics table

| Column      | Type     | Description            |
| ----------- | -------- | ---------------------- |
| id          | INTEGER  | Primary key            |
| url_id      | INTEGER  | Foreign key to urls.id |
| accessed_at | DATETIME | Access timestamp       |
| user_agent  | TEXT     | Browser user agent     |
| ip_address  | TEXT     | Client IP address      |
| referrer    | TEXT     | HTTP referrer          |

## Tech Stack

- **Backend:** Node.js + Express
- **Database:** SQLite
- **Frontend:** HTML, CSS, JavaScript (Vanilla)
- **Containerization:** Docker

## Environment Variables

- `DB_PATH` - Database file path (default: `./urls.db`)
- `NODE_ENV` - Node environment
- `PORT` - Server port (default: 2020)

## Project Structure

```
.
├── server.js           # Express server & API routes
├── database.js         # SQLite database setup
├── package.json        # Dependencies
├── Dockerfile          # Docker image definition
├── docker-compose.yml  # Docker Compose configuration
├── public/
│   ├── index.html      # Frontend UI
│   ├── style.css       # Styling
│   └── script.js       # Client-side logic
└── data/               # Database storage (Docker volume)
```

## Author

Built with ❤️ for DevOps learning

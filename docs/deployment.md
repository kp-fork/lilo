# Deployment

## Railway

Railway is the recommended hosted setup:

```bash
./scripts/setup-railway.sh
```

The interactive setup script will:

- Link or create a Railway project named `lilo`
- Prompt for the GitHub repo to connect
- Set core env vars
- Mount a persistent volume at `/data` for `LILO_WORKSPACE_DIR` and
  `LILO_SESSIONS_DIR`
- Generate a public domain on port `8080`

You still configure optional message-channel keys, such as Resend, Twilio,
Telegram, and Firecrawl, from the Railway dashboard.

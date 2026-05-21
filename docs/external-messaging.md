# External Messaging

Lilo can be an email, WhatsApp, or Telegram chatbot. Each channel is opt-in:
leave its env vars unset and it is disabled.

Telegram setup lives in the main [README](../README.md#telegram-setup).

## Native app links

Messaging channels can include buttons that open workspace apps or files in the
native iOS app. For multi-workspace or self-hosted installs, use the separate
minimal broker service in [`link-broker/`](../link-broker/) as the single
Universal Link domain for the app.

Set these on each Lilo workspace backend that should generate native app links:

| Variable               | Description                                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| `LILO_PUBLIC_APP_URL`  | Public HTTPS origin for this Lilo workspace. Used to tell the native app which workspace should handle a link. |
| `LILO_LINK_BROKER_URL` | Public HTTPS origin of the link broker. When set, workspace links in Telegram replies are sent through it.     |

Set this on the link broker service, not on every workspace backend:

| Variable                          | Description                                                                                   |
| --------------------------------- | --------------------------------------------------------------------------------------------- |
| `LILO_IOS_UNIVERSAL_LINK_APP_IDS` | Comma-separated Apple app IDs in `TEAM_ID.bundle.identifier` format to advertise in the AASA. |

The iOS app entitlement should contain the broker domain, for example
`applinks:<broker-domain>`. Only set `LILO_IOS_UNIVERSAL_LINK_APP_IDS` on the
workspace backend if you intentionally want that backend to serve its own
`apple-app-site-association` file instead of using the broker.

## Email with Resend

```bash
RESEND_API_KEY=re_...
RESEND_WEBHOOK_SECRET=whsec_...
LILO_EMAIL_AGENT_ADDRESS=hi@yourdomain.com        # your bot's inbound address
LILO_EMAIL_REPLY_FROM="Lilo <lilo@yourdomain.com>"
LILO_EMAIL_ALLOWED_SENDERS=you@yours.com,partner@theirs.com   # allowlist
LILO_PUBLIC_APP_URL=https://your-lilo.example.com # optional; adds chat permalinks and native app links
```

1. Set up a receiving domain in Resend.
2. Create a webhook pointing to `https://your-lilo/api/inbound-email` with the
   `email.received` event.
3. Send Lilo an email; it replies in-thread.

Replies set `Reply-To: LILO_EMAIL_AGENT_ADDRESS`, so the recipient's reply
round-trips back into the same inbox.

## WhatsApp with Twilio

```bash
TWILIO_ACCOUNT_SID=AC...
TWILIO_AUTH_TOKEN=...
LILO_WHATSAPP_AGENT_NUMBER=whatsapp:+15555550123
LILO_WHATSAPP_ALLOWED_SENDERS=whatsapp:+15555550124
```

Point a Twilio WhatsApp webhook at `https://your-lilo/api/inbound-whatsapp`.

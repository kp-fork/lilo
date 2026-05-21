# Mobile App

Lilo works well as an iPhone home-screen app. It still needs your Lilo backend
to be running; this is an app-like Safari wrapper, not an offline native app.

1. Deploy Lilo somewhere your phone can reach, ideally over HTTPS. Railway's
   generated public domain works well.
2. On your iPhone, open the Lilo URL in Safari. Use Safari specifically; other
   iOS browsers do not expose the same Add to Home Screen flow.
3. Log in if you configured `LILO_AUTH_PASSWORD`.
4. Tap the Share button, then tap **Add to Home Screen**.
5. Name it `Lilo`, tap **Add**, and launch it from your home screen.

# Workspace apps

The most distinctive thing about Lilo: **the agent builds its own apps**. Each
app lives as a directory of HTML and assets under `$LILO_WORKSPACE_DIR/`, runs
in a sandboxed iframe, and can read/write its own files, open chats, and make
HTTP calls through a built-in `window.lilo` API.

Ask the agent *"build me a habit tracker"* and it scaffolds one. No build step.

A workspace app is just a directory under `$LILO_WORKSPACE_DIR/`:

```
workspace/
├── todo/
│   ├── index.html
│   ├── manifest.json    # { "name": "TODO", "icon": "icon.png" }
│   └── icon.png
├── calories/
│   └── index.html
└── …
```

Each app is served at `http://localhost:8787/workspace/<app-name>/` and
rendered inside the Lilo viewer in a sandboxed iframe. Apps can:

- **Read/write their own files** through a built-in `window.lilo.fs` API
- **Open new chats** via `window.lilo.os.chats.create(...)` — used by the
default Desktop's "Chat with Lilo" prompt box
- **Call other apps** (e.g. open another file in the viewer)
- **Make HTTP requests** through the backend's proxy, so they can talk to
external APIs without CORS pain

The agent writes HTML and JavaScript directly into the app directory and opens
it in the viewer.

## Element picker

Click the cursor icon in the composer while an app is open, hover any element
in the app, and click. Its HTML, tag, text preview, and screenshot are
attached to your next message — so *"make this button bigger"* actually means
something.

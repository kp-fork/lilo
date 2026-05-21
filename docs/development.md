# Development

From the repo root:

```bash
pnpm run dev            # run backend + frontend + live typechecks in parallel
pnpm run dev:backend    # port 8787
pnpm run dev:frontend   # port 5800
pnpm run dev:template   # use the bundled template as the workspace
pnpm run build          # build both packages
pnpm run lint           # oxlint across the repo
pnpm run format         # oxfmt across the repo
```

`pnpm run dev:template` points `LILO_WORKSPACE_DIR` at the bundled template,
which is useful for trying the default apps without polluting your own
workspace.

# obsidian-open

A one-page redirect that makes Obsidian notes clickable from GitHub, which strips `obsidian://` links.

Link format: `https://robbieh-noname.github.io/obsidian-open/#<URL-encoded vault-relative path>` (no `.md`), e.g. `#Knowledge_Base%2FREADME`.
The page opens `obsidian://open?vault=Work&file=<path>`, then returns to the previous page once Obsidian takes focus (or closes the tab if it was opened in a new one). The path stays in the URL fragment, so it is never sent to the server.

One-time setup per browser: open a link with `?setup` before the `#` (e.g. `https://robbieh-noname.github.io/obsidian-open/?setup#Knowledge_Base%2FREADME`) and tick "Always allow … to open links of this type". Without that, the "Open Obsidian?" prompt takes focus, the automatic return fires, and the prompt is dismissed before you can click it.

## Making a link

Encode the vault-relative path (no `.md`) with every `/`, space and symbol escaped:

```
python3 -c 'import sys,urllib.parse; print("https://robbieh-noname.github.io/obsidian-open/#"+urllib.parse.quote(sys.argv[1], safe=""))' 'Knowledge_Base/Scan Engine/README'
```

Use it as a normal markdown link, `[label](https://robbieh-noname.github.io/obsidian-open/#…)`. Renaming or moving the note in Obsidian breaks existing links.

## Editing this page

- There's no permanent local checkout; clone it fresh (`gh repo clone robbieh-noname/obsidian-open`) and push to `main`. Pages redeploys in about two minutes.
- GitHub Pages serves the page with `cache-control: max-age=600`, so a browser can keep running the old version for up to 10 minutes after a deploy. Before testing a change, force-reload the bare page (Cmd+Shift+R on `https://robbieh-noname.github.io/obsidian-open/`) or wait it out; check what the server sends with `curl -s <url> | grep <new text>`.
- The automatic return triggers on the page losing focus. Chrome's "Open Obsidian?" prompt also takes focus, so any return logic that fires on focus loss dismisses the prompt unless "Always allow" is already ticked (the `?setup` step above). Polling `document.hasFocus()` and returning on re-focus both failed in Chrome for the same reason.

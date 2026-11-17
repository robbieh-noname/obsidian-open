# obsidian-open

A one-page redirect that makes Obsidian notes clickable from GitHub, which strips `obsidian://` links.

Link format: `https://robbieh-noname.github.io/obsidian-open/#<URL-encoded vault-relative path>` (no `.md`), e.g. `#Knowledge_Base%2FREADME`.
The page opens `obsidian://open?vault=Work&file=<path>`, then returns to the previous page when you switch back to the browser (or closes the tab if it was opened in a new one). The path stays in the URL fragment, so it is never sent to the server.

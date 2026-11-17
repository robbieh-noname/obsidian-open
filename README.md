# obsidian-open

A one-page redirect that makes Obsidian notes clickable from GitHub, which strips `obsidian://` links.

Link format: `https://robbieh-noname.github.io/obsidian-open/#<URL-encoded vault-relative path>` (no `.md`), e.g. `#Knowledge_Base%2FREADME`.
The page opens `obsidian://open?vault=Work&file=<path>`. The path stays in the URL fragment, so it is never sent to the server.

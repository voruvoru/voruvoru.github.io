# Chibi Wibu Art Backoffice

- Open `admin.html`
- Username: `admin`
- Password: `123`
- Edit content and click **Save Draft** / **Preview Site**.
- To publish globally on GitHub Pages, enter GitHub owner, repository, branch and a Personal Access Token with Contents write permission, then click **Publish to GitHub**.
- The token is kept in `sessionStorage` only and is never committed into the site.

## Security warning
The `admin / 123` login is client-side because this project is static GitHub Pages. Anyone who can inspect `admin.html` can discover it. It is therefore a convenience gate, not real authentication. Real secure backoffice login requires a backend/auth provider (for example Cloudflare Access, Firebase Auth, Supabase Auth, Netlify Identity, or a server-side admin app).

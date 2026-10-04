# VoruVoru content editor

Open admin.html. The existing convenience login is admin / 123; this static client-side gate is not secure authentication. Save Draft and Preview Site use the same voruvoruCmsDraft key. Invalid drafts fall back to the public CMS data.

To publish without a token: click Download cms-data.json, upload that file at the repository root in GitHub, and commit to main. Upload real owned artwork under assets first and enter its path in the editor. Pending image files must be published before draft/export. Direct token-based publishing remains optional; no token is needed for browser uploads.

Articles/news editing changes cards; their linked HTML files must also exist. Logout clears the session connection. Real secure admin access requires a backend or an authentication provider.

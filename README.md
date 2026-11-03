# Talaria apps catalog

Outcrop Labs' default app catalog for [Talaria](https://github.com/outcrop-labs/talaria).
Every Talaria instance lists this catalog in **Manage → Apps → Discover**, and reads it from:

```
https://raw.githubusercontent.com/outcrop-labs/talaria-apps/main/index.json
```

An admin can add more catalogs or remove this one. Installing from a Git URL works without any catalog.

## The index

`index.json` is one object with an `apps` list. Each entry:

| Field | Required | Meaning |
|---|---|---|
| `slug` | yes | The app's slug, the same as `slug` in its `talaria.json`. |
| `name` | yes | The name Discover shows. |
| `repo` | yes | The app's public `https://` git URL. |
| `description` | no | One or two sentences. |
| `icon` | no | One emoji. Defaults to ⬡. |
| `author` | no | Who maintains it. Defaults to `community`. |
| `official` | no | `true` only for apps Outcrop Labs maintains. |
| `version` | no | The version to show. |

An entry without a valid slug, a name and an `https://` repo is skipped. A file that is not
`{"apps": [...]}` makes the whole catalog read as an error.

```json
{
  "apps": [
    {
      "slug": "notes",
      "name": "Notes",
      "repo": "https://github.com/example/talaria-app-notes",
      "description": "Shared notes for a team.",
      "icon": "📝",
      "author": "Example Co"
    }
  ]
}
```

## Listing an app

1. Publish the app as a public git repository with `talaria.json` at its root, and check it with
   the SDK kit (`talaria-app check && talaria-app build && talaria-app eval`). See
   [Publishing an app](https://github.com/outcrop-labs/talaria/blob/main/docs/APPS.md#publishing-an-app).
2. Open a pull request here that adds its entry to `index.json`.

Installing an app adds code that runs fully trusted inside a Talaria deployment. Every listing is
reviewed before it is merged, and only apps Outcrop Labs maintains are marked `official`.

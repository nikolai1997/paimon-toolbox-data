# genshin-toolbox-data

Remote data repository for Genshin Toolbox.

This repository hosts generated JSON files for the app update pipeline:

- `data/public/metadata.json`: combined character, weapon, and material database
- `data/public/announcements.json`: announcement feed
- `data/public/gacha-events.json`: gacha pool/event data
- `data/public/config.json`: remote configuration
- `data/public/latest.json`: data/version check
- `data/public/manifest.json`: integrity manifest for every public data file
- `data/releases/data-pack-*.zip`: offline import packages

## Update Model

The current source strategy is:

1. Official announcement API plus manual patch JSON.
2. Generated public JSON and offline zip are committed back to this repository.
3. GitHub Pages publishes `data/public` as the app-facing endpoint.

The app should use:

```text
https://nikolai1997.github.io/genshin-toolbox-data/metadata.json
```

If GitHub Pages is not reachable for a user, publish the newest
`data/releases/data-pack-*.zip` to a domestic netdisk and let the app import it
as an offline data package.

## Manual Update

```bash
python3 tools/update_remote_data.py \
  --source official-manual \
  --manual-dir data/manual \
  --fetch-official-announcements \
  --public-dir data/public \
  --release-dir data/releases
```

## Notes

Do not put account cookies, API keys, or private user data in this repository.
All files here are intended to be public.

<div align="center">

<img src="https://r2.fivemanage.com/GPYOH8Hq4GPyAY7czrgLe/pulsarbanner.png" alt="Pulsar Framework" width="100%" />

<br/>

# PULSAR-TXADMINRECIPE

### txAdmin deploy recipe for the Pulsar Framework — sql, server.cfg, resources.cfg, and every pulsar_* resource

<br/>

![YAML](https://img.shields.io/badge/txAdmin-Recipe-2C2D72?style=flat-square)
![FiveM](https://img.shields.io/badge/FiveM-F40552?style=flat-square)

<br/>

<sub>Enjoy the framework? A coffee helps keep active development, hardening, and support going.</sub>

<a href="https://buymeacoffee.com/pulsarframework"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 50px !important;width: 180px !important;" /></a>

<br/>

[Overview](#overview) · [What This Recipe Does](#what-this-recipe-does) · [pulsarsql](#pulsarsql) · [Not Included](#not-included--do-this-manually-after-deploy) · [Maintaining](#maintaining-this-recipe)

</div>

---

## Overview

This recipe runs inside [**txAdmin**](https://github.com/tabarra/txAdmin). Please check the [**Recipe Documentation Page**](https://github.com/tabarra/txAdmin/blob/master/docs/recipe.md).

It deploys a complete Pulsar Framework server — jobs, gangs, housing, crime, and more — by pulling every `pulsar_*` resource from its own GitHub repo, wiring up third-party dependencies, and importing the database schema.

---

## What This Recipe Does

- Deploys `server.cfg` and `resources.cfg`
- Imports `pulsar.sql` (trimmed schema — see below)
- Pulls `citizenfx/cfx-server-data` for the base cfx resources (mapmanager, spawnmanager, yarn, fivem-map-hipster, etc)
- Pulls third-party dependencies we don't own (`oxmysql`, `screencapture`, `discord-screenshot`) from their own latest releases
- Pulls every `pulsar_*` resource from its own repo's latest GitHub release (`PulsarFW/<resource>`)

---

## `pulsar.sql`

This is **not** a full dump — it's trimmed. A number of tables are self-provisioned at runtime by their owning resource (`CREATE TABLE IF NOT EXISTS` on first use), so shipping them here just bloats the recipe and slows down txAdmin imports on large databases. Tables that self-seed (org bank accounts, default jobs, spawn points, etc.) are intentionally left for the resources to create themselves on first boot — don't re-add pre-seeded data to this file without checking whether the owning resource already handles it.

---

## Not Included — do this manually after deploy

- **`[assets]`** (`[custom-maps]` + `[pulsar-assets]`) — not tracked in any of the per-resource repos, copy it into `resources/[assets]` yourself.
- **`sv_licenseKey`** and **`steam_webApiKey`** in `server.cfg` are placeholders (`"changeme"`) — get your own at [keymaster.fivem.net](https://keymaster.fivem.net/) and [steamcommunity.com/dev/apikey](https://steamcommunity.com/dev/apikey) and fill them in before starting the server.
- Discord webhook URLs, phone selfie webhook/token, and API endpoint/secret in `server.cfg` are also left blank/placeholder — fill in whichever integrations you actually use.

---

## Maintaining This Recipe

- If a `pulsar_*` resource gets renamed, added, or removed from `resources.cfg`, update `pulsar.yaml`'s task list (and `resources.cfg` itself) to match — the recipe doesn't discover resources automatically, it's an explicit list.
- Every `pulsar_*` download depends on that resource's GitHub Actions release workflow having actually run and published a `<name>.zip` asset. If a resource has no release yet, its `download_file` task will fail the whole recipe at that step.
- This recipe's own `pulsar.yaml` self-downloads from `https://github.com/Artmines/TxAdminRecipie` (matching every other `pulsar_*` resource's self-hosted-repo pattern) — that repo needs to contain this folder's contents (`pulsar.yaml`, `pulsar.sql`, `server.cfg`, `resources.cfg`) at its root. Deploy via URL in txAdmin using the raw file link: `https://raw.githubusercontent.com/Artmines/TxAdminRecipie/main/pulsar.yaml`

---

<div align="center">

![Pulsar Framework](https://img.shields.io/badge/Pulsar-Framework-7c3aed?style=flat-square)
![Built for FiveM](https://img.shields.io/badge/Built_for-FiveM-F40552?style=flat-square)

</div>

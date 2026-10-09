# kiwi-web-catalog

The web side of the [Kiwi Network](https://kiwi-network.eu): hubs built on [kiwi-framework](https://github.com/derlocke-ng/kiwi-framework), the apps they ship, and the framework itself. The same shape as [kiwi-catalog](https://github.com/derlocke-ng/kiwi-catalog), which lists desktop apps for the kiwi updater: a git repository you can read, fork and send a pull request to. No accounts, no store.

- `apps.list`: one git URL per line, with options after it (`path=` for an app inside a hub's repository, `ref=` to pin a version). Comments in the file explain the categories.
- `catalog.manifest`: this catalog's own name and maintainer.
- Every listed repository (or the folder `path=` names) carries a `kiwi.manifest` with `NAME`, `DESCRIPTION`, `VERSION`, `CATEGORY` (`Framework`, `Hub` or `App`), `COMPONENTS=web`, `TAGS`, `HOMEPAGE`, `LICENSE`, and for hubs and apps the framework they are built on (`FRAMEWORK`). Apps also name the nostr event kinds they speak (`KINDS`) so a hub knows what a mount will read and write.

## What the catalog is for

A hub shows **mounts**: app code on a space (a community with its own relays and moderators). Importing another hub's store or feed is one mount line in that hub's `distribution.js`; if the code is not one the hub already ships, the catalog is where it finds the repository. Federation is this list plus the relays: nothing is blended, nothing arrives unasked. The model is in the framework's [`docs/architecture.md`](https://github.com/derlocke-ng/kiwi-framework/blob/main/docs/architecture.md), under *Mounts* and *Catalogs and kiwi*.

## Adding an entry

Fork, add a line to `apps.list`, make sure the repository has its `kiwi.manifest`, and open a pull request. Hubs are listed once; their apps once each with `path=` unless the app has a repository of its own. Releases are git tags (`v1.2.3`); entries without tags follow `HEAD`.

Not for the desktop updater: these entries have no `install.sh`, so do not add this catalog with `kiwi catalog add`. The kiwi-server module that installs a hub onto a node will read it when it exists.

## License

The catalog files are public domain (CC0). Every listed project has its own license, named in its manifest.

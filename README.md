[![Track upstream release and build .deb](https://github.com/EvilSupahFly/transmission/actions/workflows/build-dep.yml/badge.svg)](https://github.com/EvilSupahFly/transmission/actions/workflows/build-dep.yml)

## Installing the built packages

Every automated run publishes its output as a GitHub Release with individual `.deb`
files attached - no need to build locally to use this.

1. Open the [latest release](../../releases/latest).
2. Download **all** the `.deb` assets into their own folder (skip the two
   `Source code` archives - those aren't needed for installing). Transmission's
   packaging splits into several packages that depend on each other
   (`transmission-common`, `transmission-gtk`, `transmission-qt`, etc.) - grab the
   whole set together rather than just the one client you want, so nothing's
   missing mid-install. `transmission-common` is required regardless of which
   client(s) you use.
3. From inside that folder, install with whichever tool you're comfortable with:

   **apt** (recommended - resolves dependencies across the whole batch of local
   files in one transaction):
```bash
   sudo apt install ./*.deb
```

   **dpkg**, classic two-step (what this build was actually validated with):
```bash
   sudo dpkg -i *.deb
   sudo apt-get install -f   # only if dpkg reports anything missing
```

   **GDebi** - convenient for a single package via double-click, but its
   dependency resolution checks your configured repos, not sibling files in the
   same folder. If you're installing several of these local `.deb`s together,
   install `transmission-common` first, then the rest - or just use `apt`/`dpkg`
   above, which treat the whole folder as one batch.

No need to remove any existing repo version first - since the local build's
version number sorts higher, installing over it is a normal in-place upgrade; the
package manager replaces the old files cleanly on its own.
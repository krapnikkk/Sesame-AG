# Fork APK builds

This fork builds Debug APKs when commits are pushed to `dev`, or through Actions > Build dev APK > Run workflow (select `dev`).

Sync upstream `dev` into this fork before building new upstream changes. Upstream pushes alone do not trigger this fork.

The workflow uses the dev toolchain and bundled native libraries (`CI=true`), generates all ABI variants plus a universal APK, and uploads APKs with SHA-256 checksums as a seven-day Actions artifact.

These are debug-signed builds, not official releases. Fresh runners may generate different debug keys, so subsequent APKs are not guaranteed to install over earlier builds. Device and module behavior require separate testing.

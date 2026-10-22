# Automatic upstream dev Release APK builds

The default branch is dev. GitHub Actions checks upstream Sesame-AG/Sesame-AG dev at minute 23 every hour (UTC). Scheduled runs may be delayed by GitHub; inactive public forks may have schedules disabled after 60 days.

Each run merges upstream dev into this fork, preserving fork commits without force pushes. Merge conflicts fail visibly and require resolution. A new upstream commit is built in the same workflow because pushes made using GITHUB_TOKEN do not trigger a second workflow. Successful upstream commits are recorded as apk-release-<upstream SHA> tags. Unchanged upstream is skipped; failed builds retry on subsequent checks. Manual runs and pushes to dev always build.

Builds use assembleRelease with upstream shrinking/minification, then re-sign all APKs with this fork's persistent PKCS12 key stored in GitHub Secrets (RELEASE_KEYSTORE_BASE64 and RELEASE_KEYSTORE_PASSWORD). RELEASE_CERT_SHA256 stores the public fingerprint. Every APK must pass apksigner verification, fingerprint comparison, and a check that it is not debuggable before upload.

Download Sesame-AG-release-<run number> from the successful Actions run. Artifacts contain architecture-specific and universal APKs, SHA256SUMS.txt and BUILD-INFO.txt, retained for 30 days. No upstream official signing identity is claimed or injected. These self-signed Release builds cannot overwrite packages signed with another key, including earlier Debug builds; back up app data before changing installations. Device/module behavior still requires device testing.

Keep a secure backup of the signing key and password: losing them prevents signing compatible updates. Never commit them to Git.

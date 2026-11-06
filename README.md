# texturecraft-builds

Build and test runner for branches of [Rebornim/texturecraft](https://github.com/Rebornim/texturecraft) (a fork of storytold/texturecraft). It holds no TextureCraft code: one manually started workflow checks out a branch, runs one job on GitHub's machines and uploads the result.

```
gh workflow run run.yml -R Rebornim/texturecraft-builds -f ref=<branch> -f job=exe
gh workflow run run.yml -R Rebornim/texturecraft-builds -f ref=<branch> -f job=test -f args="-p texturecraft-engine --test session"
gh workflow run run.yml -R Rebornim/texturecraft-builds -f ref=<branch> -f job=snapshots -f args="-p texturecraft-ui-egui --test ui_snapshots -- --ignored"
```

- `exe`: Windows release build of the desktop app, uploaded as the artifact `texturecraft-exe`.
- `test`: `cargo test <args>` on Ubuntu; the log is uploaded as `test-log`.
- `snapshots`: like `test`, with a software Vulkan driver and `TC_UI_SNAPSHOTS=out`; the pictures are uploaded as `snapshots`.

The full quality gate stays in the fork's own CI (`ci.yml`, `cargo xtask ci`).

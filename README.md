# renovate-config

Shared [Renovate](https://docs.renovatebot.com/config-presets/) preset for the ray-manaloto projects. It is our
own trimmed copy of [risu729/renovate-config](https://github.com/risu729/renovate-config) (MIT), not a chain to it.

## Usage

In the project's `renovate.json5`:

```json5
{
	$schema: "https://docs.renovatebot.com/renovate-schema.json",
	extends: ["github>ray-manaloto/renovate-config#v1.0.0"],
}
```

Renovate bumps that tag when this repository releases a new one. This repository uses its own preset from `main`.

## What the preset does

- Extends `config:best-practices` and pins versions.
- Automerges minor, patch and digest updates through GitHub's native auto-merge. GitHub waits only for
  **required** checks, so each project must make its CI check required on the default branch.
- **No release cooldown:** an update opens as soon as a release is out (`minimumReleaseAge: "0 days"`).
- Removes the hourly and concurrent PR limits.
- Lock file maintenance runs daily and automerges, so tools pinned as `latest` are refreshed in lock files.
- Custom managers: the hk Pkl package imports in `hk.pkl`, the
  [ray-manaloto/hk-config](https://github.com/ray-manaloto/hk-config) raw-URL imports, and the mise `version`
  in `jdx/mise-action` steps.
- Groups mise's GitHub release and Docker image, hk, hk-config and usage updates.

## Checks

`mise run check` validates `default.json` and this repository's own config with `renovate-config-validator
--strict`. CI runs it on GitHub-hosted runners; the `CI Check` job is the one required check.

## License

[MIT](LICENSE). Derived from risu729/renovate-config.

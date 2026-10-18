# Renovate config

> [Renovate](https://renovatebot.com/) is a bot that automates dependencies updates. It allows you to stay up-to-date with the latest releases automatically.

This repository contains my personal [Renovate config preset](https://docs.renovatebot.com/config-presets/) for my projects but you're free to use it if you want!

## Usage

Add the following to your `renovate.json` file:

```json
{
  "extends": ["github>barbapapazes/renovate-config"]
}
```

## Auto-merge

The shared preset enables PR auto-merge only for patch and minor updates across all package managers, including pre-1.0 packages. Major updates are never auto-merged by this preset. Other update types, including pin, digest, and lock file maintenance, also require manual merging. This also applies to this repository, which extends the same preset.

Renovate does not ignore tests. Configure required status checks and branch protection in each consuming repository to enforce your merge requirements. When using GitHub's native auto-merge, enable **Allow auto-merge** in that repository's settings. The preset does not change repository settings or bypass merge rules.

Consuming repositories can disable patch and minor auto-merge with a package rule matching those update types and setting `"automerge": false`.

## Useful links

- [Renovate docs](https://docs.renovatebot.com/)
- [Renovate config presets](https://docs.renovatebot.com/config-presets/)

## License

[MIT](LICENSE) © [Barbapapazes](https://github.com/barbapapazes)

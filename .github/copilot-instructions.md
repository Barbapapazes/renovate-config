# Renovate Configuration Preset

This is a Renovate configuration preset repository containing shareable Renovate Bot configurations. The repository provides a preset configuration that other projects can extend to automatically manage dependency updates.

**Always reference these instructions first and only fallback to search or bash commands when you encounter unexpected information that does not match the information provided here.**

## Working Effectively

### Prerequisites
- Install pnpm package manager: `npm install -g pnpm`
- Node.js is required (already available in most environments)

### Bootstrap and Setup
Bootstrap the repository with these commands (execute in order):
1. `pnpm install` -- installs dependencies (takes ~35 seconds, includes 999 packages)
2. Validate everything is working: `pnpm run validate`

### Available Commands
- `pnpm run validate` -- validates the Renovate configuration (takes ~3 seconds)
- `pnpm run test` -- runs validation (alias for validate command, takes ~3 seconds)
- `pnpm run lint` -- lints JavaScript/JSON files with ESLint (takes ~3 seconds)
- `pnpm run lint:fix` -- lints and auto-fixes issues (takes ~3 seconds)

**All commands complete quickly (2-4 seconds). No long-running builds or processes.**

### File Structure and Key Components
- `default.json` -- Main Renovate configuration preset with package grouping rules
- `renovate.json` -- Self-referential config for this repository
- `package.json` -- Project metadata and scripts
- `eslint.config.js` -- ESLint configuration using @antfu/eslint-config
- `.github/workflows/ci.yml` -- CI pipeline that runs tests
- `.github/workflows/autofix.yml` -- Auto-formatting workflow

## Validation

### Core Functionality Testing
Always validate changes by running the complete validation suite:
1. `pnpm run validate` -- ensures Renovate config is valid
2. `pnpm run lint` -- ensures code style compliance
3. Both commands must pass for CI to succeed

### Configuration Validation
The main configuration file (`default.json`) is validated using `renovate-config-validator`. This ensures:
- JSON schema compliance
- Valid Renovate configuration syntax
- No deprecated or invalid configuration options

**Note**: The validator may show warnings about "Config migration necessary" - this is normal and indicates the config uses newer syntax patterns.

### Manual Testing Scenarios
Since this is a configuration preset, manual testing involves:
1. Validating the configuration syntax is correct
2. Ensuring all package rules are properly formatted
3. Checking that the preset can be successfully extended by other repositories

## CI/CD Requirements
Before committing changes, always run:
- `pnpm run lint:fix` -- fixes formatting issues automatically
- `pnpm run validate` -- ensures config validity
- Both commands must pass or the GitHub Actions CI will fail

The CI pipeline (.github/workflows/ci.yml) runs:
1. Install dependencies with pnpm
2. Run the test suite (which calls validate)

## Common Tasks

### Modifying Package Rules
When adding or modifying package grouping rules in `default.json`:
1. Edit the `packageRules` array
2. Ensure proper JSON syntax (no trailing commas)
3. Run `pnpm run validate` to check configuration validity
4. Run `pnpm run lint:fix` to ensure formatting consistency

### Adding New Package Groups
Each package rule in `default.json` should have:
- `groupName`: Human-readable name for the group
- `groupSlug`: Kebab-case identifier used in PR titles
- `matchDatasources`: Array specifying which package managers (e.g., "npm", "packagist")
- Matching criteria: `matchPackageNames` or `matchPackagePatterns`

### Repository Usage
This preset is used by adding to another project's `renovate.json`:
```json
{
  "extends": ["github>barbapapazes/renovate-config"]
}
```

## Troubleshooting

### Common Issues
- **Validation fails**: Check JSON syntax in `default.json`, ensure no trailing commas
- **Linting fails**: Run `pnpm run lint:fix` to auto-resolve formatting issues
- **pnpm not found**: Install with `npm install -g pnpm`

### Dependencies
- The repository uses pnpm as the package manager (specified in package.json)
- ESLint configuration uses @antfu/eslint-config preset
- Renovate package is included as a dev dependency for configuration validation

### Build Notes
- No traditional "build" process - this is a configuration-only repository
- No compiled artifacts or dist directories
- No runtime application to start or stop
- Configuration changes take effect when other repositories update their dependency on this preset

## Repository Structure Summary

```
├── .github/
│   └── workflows/          # CI/CD pipelines
├── default.json           # Main Renovate preset configuration
├── renovate.json         # Self-referential Renovate config
├── package.json          # Project metadata and scripts
├── eslint.config.js      # ESLint configuration
├── pnpm-lock.yaml        # Lock file for dependencies
├── .editorconfig         # Editor configuration
└── .gitignore           # Git ignore rules
```

## Performance Notes
- Dependency installation: ~35 seconds (999 packages)
- Configuration validation: ~3 seconds
- Linting: ~3 seconds
- Total development setup time: <1 minute
- No long-running processes or builds to wait for

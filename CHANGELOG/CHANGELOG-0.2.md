# Changelog 0.2

## [0.2.1](https://github.com/project-cdim/layout-apply-compose/compare/v0.2.0...v0.2.1) - 2026-11-02

The changes from v0.2.0 are as follows:

### Added

- Added separate rotating log output for layout design request bodies and the sample design engine.
- Added container security settings to prevent privilege escalation, drop the `NET_RAW` capability, and remove SUID/SGID permissions.

### Changed

- Updated Python from 3.14.0 to 3.14.6 and updated the layout-design and sample-design-engine-plugin submodules.
- Replaced `compose.yml` with `compose.yml.template`, added proxy build arguments, and removed the environment-specific Compose override.
- Updated the Docker image build to install the layout-design package as part of the image build.


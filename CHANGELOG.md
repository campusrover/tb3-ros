# Changelog

All notable changes to this project will be documented in this file.

## [2.1.1] - 2021-01-27

### Changed

- Removed various ROS dependencies (robot_services, rbx1, gen5).

## [2.1.0] - 2021-01-17

### Changed

- Moved Tailscale into the image itself, running an external Tailscale relay is no longer needed.

### Added

- Netcat utils.

## [2.0.0] - 2021-01-03

### Changed

- Migrated to new base image `fcwu/docker-ubuntu-vnc-desktop` instead of `coros`.
- Upgraded `code-server` to v2.

## [3.0.0] - 2022-7-17

### Changed

- Updated to Noetic and Ubuntu 20.04
- Install now noetic linux signing key so that apt-get update works



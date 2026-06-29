# Agent Guide: quay-builder-qemu

## Purpose

Builds a container image that boots Fedora CoreOS under QEMU/KVM for isolated builder workflows.

## Start Here

- Image build: `Dockerfile`
- VM boot: `start.sh`
- Build helper: `build.sh`
- Detailed flow: `ARCHITECTURE.md`

## Common Tasks

- Update CoreOS source: adjust `CHANNEL` or `CLOUD_IMAGE` handling and test a boot.
- Change VM resources: edit `VM_MEMORY`, `VM_VOLUME_SIZE`, or QEMU flags in `start.sh`.
- Debug boot: inspect userdata, QEMU flags, and stream metadata.

## Commands

```bash
TAG=test IMAGE=quay-builder-qemu ./build.sh
docker run --rm --privileged -e USERDATA="$(cat user_data)" quay-builder-qemu:test
```

## Guardrails

- Do not commit downloaded qcow2 images or userdata with secrets.
- This repo does not execute full Quay build jobs; orchestration lives in `quay-builder` and `quay/buildman`.
- QEMU flag changes affect host permissions and isolation.

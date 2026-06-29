# Contributing to quay-builder-qemu

Keep changes focused on the executor image, boot script, and CoreOS image selection. Changes to Quay build job orchestration belong in `quay-builder` or `quay/buildman`.

## Setup

You need a container runtime and host support for KVM to fully test this repository:

```bash
docker build --build-arg channel=stable -t quay-builder-qemu:test .
```

For a full boot test, run the image on a host where `/dev/kvm` is available and privileged containers are allowed.

## Testing

```bash
TAG=test IMAGE=quay-builder-qemu ./build.sh

docker run --rm --privileged \
  -e USERDATA="$(cat user_data)" \
  -e VM_MEMORY=2G \
  -e VM_VOLUME_SIZE=16G \
  quay-builder-qemu:test
```

Use minimal userdata for smoke tests, then test the real builder userdata in the downstream environment that consumes this image.

## Pull Requests

- State the Fedora CoreOS channel or image URL used for validation.
- Include whether the change affects build time, boot time, networking, disk size, or memory.
- Do not include local qcow2 files, credentials, or generated userdata.
- Ask for review from builder owners when QEMU flags or guest boot behavior changes.

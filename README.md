# Builder Image

```
docker build --build-arg channel=stable -t quay.io/quay/quay-builder-qemu-coreos:staging .
```

## Contextification Addendum

```mermaid
flowchart LR
    build[Dockerfile build]
    stream[CoreOS stream metadata]
    qcow[qcow2 image]
    image[executor image]
    userdata[USERDATA]
    qemu[QEMU/KVM guest]

    stream --> build
    build --> qcow
    qcow --> image
    userdata --> image
    image --> qemu
```

Key files: `Dockerfile`, `start.sh`, and `build.sh`. Validate image build with:

```bash
TAG=test IMAGE=quay-builder-qemu ./build.sh
```

Full validation needs a host that can run privileged containers with KVM.

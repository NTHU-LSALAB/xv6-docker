# xv6-docker

## Reminder

This repository is for TAs preparing the xv6 environment for students in the course. TAs should build and push the image to a Docker registry, and provide the full image name to students.

## Build image

```bash
docker build -t ${DOCKER_USERNAME}/xv6:riscv64 --platform linux/riscv64 -f Dockerfile.riscv .
docker build -t ${DOCKER_USERNAME}/xv6:arm64v8 --platform linux/arm64/v8 -f Dockerfile.arm64v8 .
docker build -t ${DOCKER_USERNAME}/xv6:amd64 --platform linux/amd64 -f Dockerfile.amd64 .
```

## Run container

The below is example to run riscv64 image. Replace the platform specification and image name as needed for `arm64v8` or `amd64`.

Explanation of the command:

- `-it`: Run in interactive mode with a TTY.
- `--rm`: Automatically remove the container when it exits.
- `-v $(pwd):/xv6`: Mount the current directory to `/xv6` in the container.
- `-v /xv6/mkfs`: Exclude the `mkfs` directory from being mounted.
- `-v $(pwd)/mkfs/mkfs.c:/xv6/mkfs/mkfs.c`: Mount only `mkfs/mkfs.c` file under the `mkfs` directory.
- `-w /xv6`: Set the working directory to `/xv6`.
- `--platform linux/riscv64`: Specify the platform for the container.

```bash
# MacOS and Linux
docker run -it --rm -v $(pwd):/xv6 -v /xv6/mkfs -v $(pwd)/mkfs/mkfs.c:/xv6/mkfs/mkfs.c -w /xv6 --platform linux/riscv64 ${DOCKER_USERNAME}/xv6:riscv64

# Windows PowerShell
docker run -it --rm -v ${PWD}:/xv6 -v /xv6/mkfs -v ${PWD}/mkfs/mkfs.c:/xv6/mkfs/mkfs.c -w /xv6 --platform linux/riscv64 ${DOCKER_USERNAME}/xv6:riscv64

# Windows CMD
docker run -it --rm -v %cd%:/xv6 -v /xv6/mkfs -v %cd%/mkfs/mkfs.c:/xv6/mkfs/mkfs.c -w /xv6 --platform linux/riscv64 ${DOCKER_USERNAME}/xv6:riscv64
```

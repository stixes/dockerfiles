# MotionEye

**motionEye** is a web-based frontend for (motion)[https://motion-project.github.io]. Check out the (wiki)[https://github.com/ccrisan/motioneye/wiki] for more details. Changelog is available on the (releases page)[https://github.com/ccrisan/motioneye/releases>].

from (GitHub)[https://github.com/ccrisan/motioneye]

This version was built to improve support for Nvidia CUDA hardware En-/Decoding on supported hardware, but should work without.

Bases on FFMpeg image by (jrottenberg/ffmpeg)[https://hub.docker.com/r/jrottenberg/ffmpeg] which provides excellent support for Nvidia based hardware in Docker.

Installs most recent Motion and Motioneye software binaries from respective release channels, and optimises for Docker operation.

## Using docker-compose

    version: "2.4"
    services:
      motioneye:
        image: stixes/motioneye-nvidia:latest
        restart: always
        runtime: nvidia
        environment:
          NVIDIA_VISIBLE_DEVICES: all
        volumes:
          - ./data:/var/lib/motioneye
          - ./config:/etc/motioneye
        tmpfs:
          - /tmp
        ports:
          - 8765:8765

Access and configure on http://<host-ip>:8765/

FROM jrottenberg/ffmpeg:4.1-nvidia

ENV MOTION_VERSION=4.3.2
ENV MOTIONEYE_VERSION=0.42.1

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
      python-pip python-dev curl libssl-dev libcurl4-openssl-dev libjpeg-dev \
      libavcodec57 libavdevice57 libavformat57 libavutil55 libmariadbclient18 \
      v4l-utils libmicrohttpd12 libswscale4 libwebp6 libwebpmux3 libpq5 \
      python-setuptools python-wheel build-essential \
    && curl -Lo /motion.deb https://github.com/Motion-Project/motion/releases/download/release-${MOTION_VERSION}/bionic_motion_${MOTION_VERSION}-1_amd64.deb \
    && dpkg -i /motion.deb \
    && rm -f /motion.deb \
    && pip install --no-cache-dir motioneye==${MOTIONEYE_VERSION} \
    && apt-get purge -y python-wheel build-essential \
    && apt-get autoremove --purge --yes \
    && apt-get --yes clean \
    && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin \
    && mkdir /etc/motioneye \
    && mkdir /var/lib/motioneye \
    && cp /usr/local/share/motioneye/extra/motioneye.conf.sample /etc/motioneye/motioneye.conf \
    && sed -i 's%run_path /var/run%run_path /tmp%' /etc/motioneye/motioneye.conf \
    && sed -i 's%log_path /var/log%log_path /tmp%' /etc/motioneye/motioneye.conf \
    && chown -R motion.motion /etc/motioneye /var/lib/motioneye

EXPOSE 8765

USER motion

VOLUME /var/lib/motioneye
VOLUME /etc/motioneye

ENTRYPOINT []
CMD ["meyectl", "startserver", "-c", "/etc/motioneye/motioneye.conf"]

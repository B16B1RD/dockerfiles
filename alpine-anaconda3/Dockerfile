FROM alpine:3.4

MAINTAINER Akiyoshi Sakaguchi <autumngoodluck@gmail.com>

ENV LOCALE=ja_JP \
    ENCODING=UTF-8 \
    GLIBC_VERSION=2.23-r3 \
    GLIBC_URL=https://github.com/sgerrand/alpine-pkg-glibc/releases/download \
    GLIBC_KEY=sgerrand.rsa.pub \
    MICRO_EDITOR_VERSION=1.1.2 \
    MICRO_EDITOR_URL=https://github.com/zyedidia/micro/releases/download \
    CONDA_VERSION=4.2.0 \
    CONDA_INSTALLER_URL=https://repo.continuum.io/archive \
    PATH=/opt/conda/bin:$PATH
ENV LC_ALL="${LOCALE}.${ENCODING}" \
    LANG="${LOCALE}.${ENCODING}"

RUN apk --update --no-cache add \
                                bash \
                                openssl \
                                tini \
                                libxext \
                                libsm \
                                libxrender \
                                ncurses5-widec-libs \
    && cd /tmp \
    && wget -q -O "/etc/apk/keys/${GLIBC_KEY}" "${GLIBC_URL}/${GLIBC_VERSION}/${GLIBC_KEY}" \
    && wget "${GLIBC_URL}/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk" \
    && wget "${GLIBC_URL}/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk" \
    && wget "${GLIBC_URL}/${GLIBC_VERSION}/glibc-i18n-${GLIBC_VERSION}.apk" \
    && apk add "glibc-${GLIBC_VERSION}.apk" "glibc-bin-${GLIBC_VERSION}.apk" "glibc-i18n-${GLIBC_VERSION}.apk" \
    && /usr/glibc-compat/bin/localedef -i "${LOCALE}" -f "${ENCODING}" "${LANG}" \
    && wget "${MICRO_EDITOR_URL}/v${MICRO_EDITOR_VERSION}/micro-${MICRO_EDITOR_VERSION}-linux64.tar.gz" \
    && tar xzvf "micro-${MICRO_EDITOR_VERSION}-linux64.tar.gz" \
    && cp "micro-${MICRO_EDITOR_VERSION}/micro" /usr/local/bin \
    && wget "${CONDA_INSTALLER_URL}/Anaconda3-${CONDA_VERSION}-Linux-x86_64.sh" -O anaconda.sh \
    && bash /tmp/anaconda.sh -b -p /opt/conda \
    && conda update --yes --all \
    && conda clean --yes --tarballs \
    && conda clean --yes --packages \
    && cd \
    && rm -rf /tmp/*

# Workaround
# This is a workaround to an error of "ImportError: No module named 'PyQt4'" when "import matplotlib.pyplot" is executed.
RUN conda install pyqt=4.11

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/bin/bash"]
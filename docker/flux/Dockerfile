ARG BASE_IMAGE=exaworks/sdk-base
FROM ${BASE_IMAGE}

ARG FLUX_CORE_VERSION=0.26.0
ARG FLUX_SCHED_VERSION=0.16.0

# Install Flux-core from release tarball
RUN V=$FLUX_CORE_VERSION \
   && PKG=flux-core-$V \
   && URL=https://github.com/flux-framework/flux-core/releases/download \
   && wget ${URL}/v${V}/${PKG}.tar.gz \
   && tar xvf ${PKG}.tar.gz \
   && cd ${PKG} \
   && PYTHON_VERSION=3 ./configure --prefix=/usr \
   && make -j 4 \
   && make install \
   && cd .. \
   && rm -rf flux-core-* \
   && ldconfig

# Install Flux-sched from release tarball
RUN V=$FLUX_SCHED_VERSION \
   && PKG=flux-sched-$V \
   && URL=https://github.com/flux-framework/flux-sched/releases/download \
   && wget ${URL}/v${V}/${PKG}.tar.gz \
   && tar xvf ${PKG}.tar.gz \
   && cd ${PKG} \
   && PYTHON_VERSION=3 ./configure --prefix=/usr \
   && make -j 4 \
   && make install \
   && cd .. \
   && rm -rf flux-sched-* \
   && ldconfig

COPY test.sh /
CMD /test.sh

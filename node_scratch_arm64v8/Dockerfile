FROM nnorthcutt/musl-cross-build:alpine3-16 as builder

ENV NODE_VERSION=21.7.3
ENV TARGET=aarch64-linux-musl
ENV CC=$TARGET-gcc
ENV CXX=$TARGET-g++
ENV AR=$TARGET-ar
ENV NM=$TARGET-nm
ENV ANLIB=$TARGET-ranlib
ENV LINK=$TARGET-g++
ENV CXXFLAGS="-O3 -ffunction-sections -fdata-sections"
ENV LDFLAGS="-Wl,--gc-sections,--strip-all"

COPY build_node.sh .
RUN chmod a+x ./build_node.sh && ./build_node.sh
RUN echo 'node:x--with-intl:1000:1000:Linux User,,,:/home/node:/bin/sh' > /tmp/passwd

FROM scratch

ENV NODE_VERSION=21.7.3

COPY --from=builder node-v$NODE_VERSION/out/Release/node /bin/node
COPY --from=builder /lib/ld-musl-*.so.1 /lib/
COPY --from=builder /tmp/passwd /etc/passwd

USER node

ENTRYPOINT ["node"]

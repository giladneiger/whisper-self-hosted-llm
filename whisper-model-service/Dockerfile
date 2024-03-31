FROM registry.access.redhat.com/ubi9/ubi:latest as builder

WORKDIR /app
RUN dnf install -y git make gcc gcc-c++
RUN mkdir whisper && cd whisper && git clone https://github.com/ggerganov/whisper.cpp.git . && \
    git checkout tags/v1.5.4 && \
    make && \
    cp main /app/main && \
    cp server /app/server && \
    cd ../ && rm -rf whisper

FROM registry.access.redhat.com/ubi9-minimal:latest
WORKDIR /app
COPY --from=builder /app /app
COPY run.sh /app/
ENTRYPOINT ["sh", "run.sh"]

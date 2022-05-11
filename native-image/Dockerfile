# Reference: https://sergiomartinrubio.com/articles/getting-started-with-graalvm-and-java-native/
FROM ghcr.io/graalvm/native-image:java11-21.2
WORKDIR /app
COPY ./src/main/java/ /app
RUN javac Main.java
RUN native-image Main --static

FROM alpine:3.15
# Reference: https://stackoverflow.com/a/55757473/12429735RUN
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "10001" \
    "appuser"

FROM scratch
WORKDIR /app
COPY --from=0 /app/main /app/main

COPY --from=1 /etc/passwd /etc/passwd
COPY --from=1 /etc/group /etc/group

# Use an underprivileged user.
USER appuser:appuser

ENTRYPOINT ["./main"]

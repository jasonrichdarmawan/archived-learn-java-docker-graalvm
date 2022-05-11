FROM ghcr.io/graalvm/jdk:java11-21.2
WORKDIR /app
COPY ./src/main/java /app
RUN javac Main.java
ENTRYPOINT java Main
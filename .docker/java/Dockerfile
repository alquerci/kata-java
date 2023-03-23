FROM eclipse-temurin:17.0.6_10-jdk-alpine

# Install Maven as package manager
#
RUN set -eux; \
    prefix='/usr/local'; \
    buildDeps=' \
        curl \
    '; \
    apk add --no-cache \
        $buildDeps \
    ; \
    \
    curl -sSLf https://dlcdn.apache.org/maven/maven-3/3.9.0/binaries/apache-maven-3.9.0-bin.tar.gz \
        -o maven.tar.gz; \
    tar -xf maven.tar.gz; \
    rm maven.tar.gz; \
    \
    rm -rf ${prefix}/share/apache-maven; \
    mv apache-maven-3.9.0 ${prefix}/share/apache-maven; \
    ln -s ${prefix}/share/apache-maven/bin/mvn ${prefix}/bin/; \
    \
    mvn --version; \
    :;

# Install google-java-format as cs fixer
#
RUN set -eux; \
    prefix='/usr/local'; \
    buildDeps=' \
        curl \
    '; \
    apk add --no-cache \
        $buildDeps \
    ; \
    \
    mkdir -p ${prefix}/share/google-java-format; \
    curl -sSLf https://github.com/google/google-java-format/releases/download/v1.15.0/google-java-format-1.15.0-all-deps.jar \
        -o ${prefix}/share/google-java-format/google-java-format.jar; \
    \
    { \
        echo '#! /bin/sh -eu'; \
        echo ''; \
        echo "java -jar ${prefix}/share/google-java-format/google-java-format.jar \$@"; \
    } > ${prefix}/bin/google-java-format; \
    chmod +x ${prefix}/bin/google-java-format; \
    \
    google-java-format --version; \
    :;

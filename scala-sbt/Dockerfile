# Base Image
FROM amazoncorretto:11-alpine3.18-full

# Install tools to be removed after
RUN apk update && \
    apk upgrade && \
    apk add --no-cache bash curl tar

# Scala
ENV SCALA_VERSION 2.13.6
ENV SCALA_HOME /usr/share/scala
RUN curl -fsL https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz | tar xfz - -C /usr/share && \
    mv /usr/share/scala-${SCALA_VERSION} $SCALA_HOME
ENV PATH $PATH:$SCALA_HOME/bin

# SBT
ENV SBT_VERSION 1.5.5
RUN curl -L -o sbt-$SBT_VERSION.tgz https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && \
    tar -zxvf sbt-$SBT_VERSION.tgz -C /usr/share && \
    rm sbt-$SBT_VERSION.tgz
ENV PATH $PATH:/usr/share/sbt/bin

# Clean up
RUN apk del curl tar

# Set Directory
RUN mkdir /app
WORKDIR /app

# PORT
EXPOSE 9000

# Default command
CMD ["sbt", "run",]

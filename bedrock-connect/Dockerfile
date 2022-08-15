FROM maven:3-openjdk-11 as mavenbuild
ARG bctag=1.20
WORKDIR /app

RUN curl -sLO https://github.com/Pugmatt/BedrockConnect/releases/download/${bctag}/BedrockConnect-1.0-SNAPSHOT.jar

FROM mcr.microsoft.com/java/jre:11-zulu-ubuntu

RUN mkdir -p /brc
COPY --from=mavenbuild /app/BedrockConnect-1.0-SNAPSHOT.jar /brc/

WORKDIR /brc
ENV custom_servers="/brc/custom_servers.json" featured_servers=true user_servers=true
RUN echo '[]' > ${custom_servers}
EXPOSE 19132/udp
CMD java -Xms512M -Xmx512M -jar BedrockConnect-1.0-SNAPSHOT.jar nodb=true custom_servers=${custom_servers} featured_servers=${featured_servers} user_servers=${user_servers}

FROM openjdk:11.0.9

WORKDIR /root

RUN apt update -y \
    && git clone https://github.com/ApolloFoundation/Apollo \
    && cd Apollo \
    && ./mvnw clean install

RUN unzip /root/Apollo/apl-exec/target/apollo-blockchain-1.*.*-NoOS-NoArch.zip -d /root/

COPY chains.json /root/config/chains.json
COPY apl-blockchain.properties /root/config/apl-blockchain.properties

ENV PATH /root/ApolloWallet/apollo-blockchain/bin:$PATH

ARG APL_API_PORT
ENV APL_API_PORT ${APL_API_PORT}

RUN sed -i -e 's/${APL_API_PORT}/'"${APL_API_PORT}"'/g' /root/config/apl-blockchain.properties

VOLUME ["/data"]

CMD [ "apl-run.sh", "--log-dir", "/data", "--db-dir", "/data", "--config-dir", "/root/config" ]

EXPOSE 7876


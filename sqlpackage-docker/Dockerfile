FROM ubuntu:18.04

WORKDIR /app

ARG sqlpackageUrl='https://go.microsoft.com/fwlink/?linkid=2113331'

RUN apt-get update && apt-get install -y curl unzip libunwind8 libicu60 libssl1.0-dev
RUN mkdir -p '/opt/sqlpackage' && \
    cd '/opt/sqlpackage' && \
    curl ${sqlpackageUrl} -L --output ./sqlpackage.zip && \
    unzip ./sqlpackage.zip -d . && \
    rm ./sqlpackage.zip && \
    chmod a+x ./sqlpackage

ENTRYPOINT [ "/opt/sqlpackage/sqlpackage" ]

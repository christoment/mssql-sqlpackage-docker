FROM mcr.microsoft.com/mssql/server

WORKDIR /app

ARG sqlPackageDir='/opt/sqlpackage'
ARG sqlpackageUrl='https://go.microsoft.com/fwlink/?linkid=2113331'

USER root
RUN apt-get update && apt-get install -y curl unzip libunwind8 libicu60 libssl1.0-dev
RUN mkdir -p ${sqlPackageDir} && \
    cd ${sqlPackageDir} && \
    curl ${sqlpackageUrl} -L --output ./sqlpackage.zip && \
    unzip ./sqlpackage.zip -d . && \
    rm ./sqlpackage.zip && \
    chmod a+x ./sqlpackage
RUN apt-get purge -y --auto-remove curl unzip

USER mssql
ENV PATH="${sqlPackageDir}:${PATH}"

EXPOSE 1433

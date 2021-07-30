# escape=`
ARG BASE_IMAGE
ARG MODULE_ASSETS

FROM ${MODULE_ASSETS} as module_assets

FROM $BASE_IMAGE as final

ARG MODULE_NAME

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

COPY --from=module_assets C:\module\db c:\resources\$MODULE_NAME
# Modules (Including Coveo) are already initialized in the mssql Dockerfile.
# However if your database is already initialized, you can add a mssql-init definition to your docker-compose file and pass it the coveo module to initialize only Coveo for Sitecore.
ENTRYPOINT .\DeployDatabases.ps1 -ResourcesDirectory c:\resources\$env:MODULE_NAME -SqlServer $env:SQL_SERVER -SqlAdminUser $env:SQL_ADMIN_LOGIN -SqlAdminPassword $env:SQL_ADMIN_PASSWORD -SkipStartingServer
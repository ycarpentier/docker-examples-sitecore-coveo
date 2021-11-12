# escape=`

ARG BASE_IMAGE
ARG SPE_IMAGE
ARG HORIZON_RESOURCES_IMAGE
ARG COVEO_ASSET

FROM ${SPE_IMAGE} as spe
FROM ${HORIZON_RESOURCES_IMAGE} as horizon_resourses
FROM ${COVEO_ASSET} as coveo
FROM ${BASE_IMAGE}

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Add SPE module
COPY --from=spe \module\db \spe_data
RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\spe_data; `
    Remove-Item -Path C:\spe_data -Recurse -Force;

# Add Horizon module
COPY --from=horizon_resourses \module\db \horizon_integration_data
RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\horizon_integration_data; `
    Remove-Item -Path C:\horizon_integration_data -Recurse -Force;

# Add Coveo module
COPY --from=coveo \module\db \coveo_data
RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\coveo_data; `
    Remove-Item -Path C:\coveo_data -Recurse -Force;

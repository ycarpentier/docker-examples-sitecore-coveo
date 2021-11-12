# escape=`

ARG BASE_IMAGE
ARG SPE_IMAGE
ARG TOOLING_IMAGE
ARG HORIZON_RESOURCES_IMAGE
ARG COVEO_ASSET

FROM ${TOOLING_IMAGE} as tooling
FROM ${SPE_IMAGE} as spe
FROM ${HORIZON_RESOURCES_IMAGE} as horizon_resources
FROM ${COVEO_ASSET} as coveo
FROM ${BASE_IMAGE}

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Copy development tools and entrypoint
COPY --from=tooling \tools\ \tools\

WORKDIR C:\inetpub\wwwroot

# Add SPE module
COPY --from=spe \module\cm\content .\

# Add horizon module
COPY --from=horizon_resources \module\cm\content \inetpub\wwwroot

# Add Coveo module
COPY --from=coveo \module\cm\content .\

# Copy role transforms
COPY .\transforms\ \transforms\role\

# Perform role transforms
RUN C:\tools\scripts\Invoke-XdtTransform.ps1 -Path .\ -XdtPath C:\transforms\role
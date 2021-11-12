# escape=`

ARG BASE_IMAGE
ARG TOOLING_IMAGE
ARG COVEO_ASSET

FROM ${TOOLING_IMAGE} as tooling
FROM ${COVEO_ASSET} as coveo
FROM ${BASE_IMAGE}

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Copy development tools and entrypoint
COPY --from=tooling \tools\ \tools\

WORKDIR C:\inetpub\wwwroot

# Add Coveo module
COPY --from=coveo \module\cm\content .\
ARG REPO=mcr.microsoft.com/dotnet/runtime

# Installer image
FROM arm64v8/buildpack-deps:bullseye-curl as installer

# Retrieve ASP.NET Core
RUN curl -fSL --output aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/5.0.13/aspnetcore-runtime-5.0.13-linux-arm64.tar.gz \
    && aspnetcore_sha512='757ccf8a453d8cc9075a438d02bf95bb6d3738651100de8d4ae842a97dc10d8d7507597ec9d2806a3140d8000faec602748b4585b0a644816c74ebbf7ab98719' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && tar -ozxf aspnetcore.tar.gz ./shared/Microsoft.AspNetCore.App \
    && rm aspnetcore.tar.gz


# ASP.NET Core image
FROM $REPO:5.0.13-bullseye-slim-arm64v8

ENV ASPNET_VERSION=5.0.13

COPY --from=installer ["/shared/Microsoft.AspNetCore.App", "/usr/share/dotnet/shared/Microsoft.AspNetCore.App"]

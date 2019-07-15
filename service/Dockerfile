FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY service.csproj service/
RUN dotnet restore service/service.csproj
WORKDIR /src/myMicroservice
COPY . .
RUN dotnet build service.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish service.csproj -c Release -o /app

FROM base AS final
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "service.dll"]
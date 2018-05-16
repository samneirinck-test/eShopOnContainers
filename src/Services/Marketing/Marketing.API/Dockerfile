FROM microsoft/aspnetcore:2.0.5@sha256:3dd91dfc75309d7b9b03e7ce2b5537fd0a8a51c74ba5af31f4688a600746be17 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0.5-2.1.4@sha256:8314a18ed2a4971a7628be46fecc469082afe0689815351cd9d6b62e9823eae6 AS build
WORKDIR /src
COPY . .
RUN dotnet restore -nowarn:msb3202,nu1503
WORKDIR /src/src/Services/Marketing/Marketing.API
RUN dotnet build --no-restore -c Release -o /app

FROM build AS publish
RUN dotnet publish --no-restore -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Marketing.API.dll"]

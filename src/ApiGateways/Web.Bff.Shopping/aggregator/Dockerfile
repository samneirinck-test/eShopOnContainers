FROM microsoft/aspnetcore:2.0.5@sha256:3dd91dfc75309d7b9b03e7ce2b5537fd0a8a51c74ba5af31f4688a600746be17 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0@sha256:b362e91043ad93e643b708859c7df49232da2a8bb2efac5d65a8cecb17bf2a5e AS build
WORKDIR /src
COPY . .
RUN dotnet restore -nowarn:msb3202,nu1503
WORKDIR /src/src/ApiGateways/Web.Bff.Shopping/aggregator
RUN dotnet build --no-restore -c Release -o /app

FROM build AS publish
RUN dotnet publish --no-restore -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web.Shopping.HttpAggregator.dll"]

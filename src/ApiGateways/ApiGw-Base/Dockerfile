FROM microsoft/aspnetcore:2.0@sha256:9fa051d41ecd1b417edc30bd6ba08dfd76566c5de5acdc327ec1c78396329272 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0@sha256:b362e91043ad93e643b708859c7df49232da2a8bb2efac5d65a8cecb17bf2a5e AS build
WORKDIR /src
COPY src/ApiGateways/ApiGw-Base/OcelotApiGw.csproj src/ApiGateways/ApiGw-Base/
RUN dotnet restore src/ApiGateways/ApiGw-Base/
COPY . .
WORKDIR /src/src/ApiGateways/ApiGw-Base/
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OcelotApiGw.dll"]

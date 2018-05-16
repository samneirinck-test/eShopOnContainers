FROM microsoft/aspnetcore:2.0@sha256:9fa051d41ecd1b417edc30bd6ba08dfd76566c5de5acdc327ec1c78396329272 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0@sha256:b362e91043ad93e643b708859c7df49232da2a8bb2efac5d65a8cecb17bf2a5e AS build
WORKDIR /src
COPY eShopOnContainers-ServicesAndWebApps.sln ./
COPY src/Services/Ordering/Ordering.SignalrHub/Ordering.SignalrHub.csproj src/Services/Ordering/Ordering.SignalrHub/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/src/Services/Ordering/Ordering.SignalrHub
RUN dotnet build Ordering.SignalrHub.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Ordering.SignalrHub.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Ordering.SignalrHub.dll"]

FROM microsoft/aspnetcore:1.1@sha256:ff21b2600280c8e54ad8f7a15cf5bcb7284986b6f7f3b3e1c9e815f193b05387
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", "eShopWeb.dll"]

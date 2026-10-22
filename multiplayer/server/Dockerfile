FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish multiplayer/server/Server.csproj -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app
COPY --from=build /app/publish .
COPY --from=build /src/multiplayer/server/Config ./Config
ENV ASPNETCORE_URLS=http://0.0.0.0:10000
CMD ["sh", "-c", "sed -i \"s/\\\"port\\\": 1337/\\\"port\\\": ${PORT:-10000}/\" Config/Settings.json && dotnet Server.dll"]

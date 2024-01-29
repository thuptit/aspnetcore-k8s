FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

EXPOSE 5000
ENV ASPNETCORE_URLS http://*:5000



ENV ASPNETCORE_ENVIRONMENT=Development


FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["/WebApp.csproj", "WebApp/"]
RUN dotnet restore "WebApp/WebApp.csproj"

WORKDIR "/src/WebApp"
COPY . .
WORKDIR "/src/WebApp"
RUN dotnet build "WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApp.dll"]
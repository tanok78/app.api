FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["app.api/app.api.csproj", "app.api/"]
RUN dotnet restore "app.api/app.api.csproj"
COPY . .
WORKDIR "/src/app.api"
RUN dotnet build "app.api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "app.api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "app.api.dll"]

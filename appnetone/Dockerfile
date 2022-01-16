FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["appnetone/appnetone.csproj", "appnetone/"]
RUN dotnet restore "appnetone/appnetone.csproj"
COPY . .
WORKDIR "/src/appnetone"
RUN dotnet build "appnetone.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "appnetone.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "appnetone.dll"]

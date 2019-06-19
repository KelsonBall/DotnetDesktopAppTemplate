FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Application.Server/Application.Server.csproj", "Application.Server/"]
RUN dotnet restore "Application.Server/Application.Server.csproj"
COPY . .
WORKDIR "/src/Application.Server"
RUN dotnet build "Application.Server.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Application.Server.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Application.Server.dll"]
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 44366

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Logs.Api/Logs.Api.csproj", "Logs.Api/"]
COPY ["Logs.Contracts/Logs.Contracts.csproj", "Logs.Contracts/"]
RUN dotnet restore "Logs.Api/Logs.Api.csproj"
COPY . .
WORKDIR "/src/Logs.Api"
RUN dotnet build "Logs.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Logs.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Logs.Api.dll"]
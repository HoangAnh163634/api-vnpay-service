FROM mcr.microsoft.com/dotnet/aspnet:8.0-preview AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:8.0-preview AS build
WORKDIR /src
COPY ["api-vnpay-service/api-vnpay-service.csproj", "./"]
RUN dotnet restore "api-vnpay-service.csproj"

COPY api-vnpay-service/ .  
RUN dotnet build "api-vnpay-service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "api-vnpay-service.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "api-vnpay-service.dll"]

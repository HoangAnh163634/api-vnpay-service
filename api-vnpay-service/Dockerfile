# Base runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0-preview AS base
WORKDIR /app
EXPOSE 80

# Build image
FROM mcr.microsoft.com/dotnet/sdk:8.0-preview AS build
WORKDIR /src

# Copy the .csproj file and restore dependencies
COPY ["api-vnpay-service.csproj", "./"]
RUN dotnet restore "api-vnpay-service.csproj"

# Copy the entire project and build
COPY . .
RUN dotnet build "api-vnpay-service.csproj" -c Release -o /app/build

# Publish the app
FROM build AS publish
RUN dotnet publish "api-vnpay-service.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Final runtime image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "api-vnpay-service.dll"]

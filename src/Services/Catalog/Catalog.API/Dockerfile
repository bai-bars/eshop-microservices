# Use the official .NET 9 ASP.NET Core runtime as a base image
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
USER app
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Build stage
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["Catalog.API.csproj", "./"]
RUN dotnet restore "./Catalog.API.csproj"
COPY . .
RUN dotnet publish "Catalog.API.csproj" -c ${BUILD_CONFIGURATION} -o /app/publish

# Final stage
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Catalog.API.dll"]
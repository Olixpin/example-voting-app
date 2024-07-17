# Build stage
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source

# Copy the csproj and restore as distinct layers
COPY *.csproj .
RUN dotnet restore --runtime linux-arm64

# Copy the remaining source files and build the app
COPY . .
RUN dotnet publish -c Release -o /app_output --runtime linux-arm64 --self-contained false

# Runtime stage
FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /app
COPY --from=build /app_output .
ENTRYPOINT ["dotnet", "Worker.dll"]

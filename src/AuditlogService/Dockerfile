FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
COPY Directory.Packages.props ./
WORKDIR /app

# Copy necessary files and restore as distinct layer
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build-env /app/out .


# Start
ENTRYPOINT ["dotnet", "Pitstop.AuditlogService.dll"]

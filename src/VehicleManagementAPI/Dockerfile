# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
COPY Directory.Packages.props ./
WORKDIR /app

# Copy the project files
COPY *.csproj ./
# Restore dependencies
RUN dotnet restore

# Copy the entire source code
COPY . ./

# Build the application
RUN dotnet publish -c Release -o out

# Stage 2: Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy the build output from the previous stage
COPY --from=build-env /app/out ./

# Expose the port the application will run on

EXPOSE 5000

# Set the entry point to run the application with --urls
ENTRYPOINT ["dotnet", "Pitstop.VehicleManagementAPI.dll", "--urls", "http://0.0.0.0:5000"]



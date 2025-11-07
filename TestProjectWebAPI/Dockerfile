# ==========================
# STAGE 1: Build the project
# ==========================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy and restore dependencies
COPY *.csproj .
RUN dotnet restore

# Copy the rest of the source code
COPY . .

# Publish the application to the /app directory
RUN dotnet publish -c Release -o /app

# ==========================
# STAGE 2: Run the app
# ==========================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy published files from the build stage
COPY --from=build /app .

# Expose the default port for ASP.NET
EXPOSE 8080

# Start the application
ENTRYPOINT ["dotnet", "TestProjectWebAPI.dll"]

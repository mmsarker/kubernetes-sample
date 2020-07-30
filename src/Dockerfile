FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY ./Mizan.Test.WebApp/*.csproj ./Mizan.Test.WebApp/
RUN dotnet restore ./Mizan.Test.WebApp/

# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 as TestWebApp
WORKDIR /app
COPY --from=build-env /app/out .
ENV ASPNETCORE_URLS http://*:8080
ENTRYPOINT ["dotnet", "Mizan.Test.WebApp.dll"]
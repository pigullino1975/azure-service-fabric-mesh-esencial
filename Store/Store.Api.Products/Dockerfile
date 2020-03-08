#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Store.Api.Products/Store.Api.Products.csproj", "Store.Api.Products/"]
RUN dotnet restore "Store.Api.Products/Store.Api.Products.csproj"
COPY . .
WORKDIR "/src/Store.Api.Products"
RUN dotnet build "Store.Api.Products.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Store.Api.Products.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Store.Api.Products.dll"]
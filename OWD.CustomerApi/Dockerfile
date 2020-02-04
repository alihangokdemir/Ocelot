#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["OWD.CustomerApi/OWD.CustomerApi.csproj", "OWD.CustomerApi/"]
RUN dotnet restore "OWD.CustomerApi/OWD.CustomerApi.csproj"
COPY . .
WORKDIR "/src/OWD.CustomerApi"
RUN dotnet build "OWD.CustomerApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OWD.CustomerApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OWD.CustomerApi.dll"]

#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApiDockerHadson/WebApiDockerHadson.csproj", "WebApiDockerHadson/"]
RUN dotnet restore "WebApiDockerHadson/WebApiDockerHadson.csproj"
COPY . .
WORKDIR "/src/WebApiDockerHadson"
RUN dotnet build "WebApiDockerHadson.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApiDockerHadson.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApiDockerHadson.dll"]
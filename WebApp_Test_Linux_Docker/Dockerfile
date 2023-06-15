#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApp_Test_Linux_Docker/WebApp_Test_Linux_Docker.csproj", "WebApp_Test_Linux_Docker/"]
RUN dotnet restore "WebApp_Test_Linux_Docker/WebApp_Test_Linux_Docker.csproj"
COPY . .
WORKDIR "/src/WebApp_Test_Linux_Docker"
RUN dotnet build "WebApp_Test_Linux_Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApp_Test_Linux_Docker.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApp_Test_Linux_Docker.dll"]
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
#EXPOSE 9080
#EXPOSE 9443
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["one/one.csproj", "one/"]
RUN dotnet restore "one/one.csproj"
COPY . .
WORKDIR "/src/one"
RUN dotnet build "one.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "one.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "one.dll", "--urls", "http://+:9080;https://+:9443"]
#ENTRYPOINT ["dotnet", "one.dll", "--urls", "http://+:9080"]
ENTRYPOINT ["dotnet", "one.dll", "--urls", "http://+:80;https://+:443"]
#ENTRYPOINT ["dotnet", "one.dll", "--urls", "http://+:80"]
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["FantasiaBit/FantasiaBit.csproj", "FantasiaBit/"]
RUN dotnet restore "FantasiaBit/FantasiaBit.csproj"
COPY . .
WORKDIR "/src/FantasiaBit"
RUN dotnet build "FantasiaBit.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FantasiaBit.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FantasiaBit.dll"]
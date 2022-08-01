#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["src/services/MS.Consult.API/MS.Consult.API.csproj", "src/services/MS.Consult.API/"]
RUN dotnet restore "src/services/MS.Consult.API/MS.Consult.API.csproj"
COPY . .
WORKDIR "/src/src/services/MS.Consult.API"
RUN dotnet build "MS.Consult.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MS.Consult.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MS.Consult.API.dll"]
FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["CoreDocker.csproj", "./"]
RUN dotnet restore "./CoreDocker.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "CoreDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CoreDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CoreDocker.dll"]

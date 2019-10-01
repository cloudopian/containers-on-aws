FROM mcr.microsoft.com/dotnet/core/runtime:2.2 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["MyBatchApp.csproj", "./"]
RUN dotnet restore "./MyBatchApp.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "MyBatchApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyBatchApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyBatchApp.dll"]

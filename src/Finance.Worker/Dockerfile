FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/Finance.Worker/Finance.Worker.csproj", "src/Finance.Worker/"]
RUN dotnet restore "src/Finance.Worker/Finance.Worker.csproj"
COPY . .
WORKDIR "/src/src/Finance.Worker"
RUN dotnet build "Finance.Worker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Finance.Worker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Finance.Worker.dll"]

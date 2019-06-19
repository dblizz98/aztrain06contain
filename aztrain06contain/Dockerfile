FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["aztrain06contain/aztrain06contain.csproj", "aztrain06contain/"]
RUN dotnet restore "aztrain06contain/aztrain06contain.csproj"
COPY . .
WORKDIR "/src/aztrain06contain"
RUN dotnet build "aztrain06contain.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aztrain06contain.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aztrain06contain.dll"]
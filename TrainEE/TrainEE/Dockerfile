FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["TrainEE/TrainEE.csproj", "TrainEE/"]
RUN dotnet restore "TrainEE/TrainEE.csproj"
COPY . .
WORKDIR "/src/TrainEE"
RUN dotnet build "TrainEE.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TrainEE.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TrainEE.dll"]

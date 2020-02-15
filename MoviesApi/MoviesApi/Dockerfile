FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["MoviesApi/MoviesApi.csproj", "MoviesApi/"]
RUN dotnet restore "MoviesApi/MoviesApi.csproj"
COPY . .
WORKDIR "/src/MoviesApi"
RUN dotnet build "MoviesApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MoviesApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MoviesApi.dll"]
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TapCounter.Web/TapCounter.Web.csproj", "TapCounter.Web/"]
RUN dotnet restore "TapCounter.Web/TapCounter.Web.csproj"
COPY . .
WORKDIR "/src/TapCounter.Web"
RUN dotnet build "TapCounter.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TapCounter.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TapCounter.Web.dll"]

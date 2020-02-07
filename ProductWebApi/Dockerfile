FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["ProductWebApi/ProductWebApi.csproj", "ProductWebApi/"]
RUN dotnet restore "ProductWebApi/ProductWebApi.csproj"
COPY . .
WORKDIR "/src/ProductWebApi"
RUN dotnet build "ProductWebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ProductWebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ProductWebApi.dll"]
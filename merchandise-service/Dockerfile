﻿FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

WORKDIR /src
COPY ["MerchandiseService/MerchandiseService.csproj", "MerchandiseService/"]
RUN dotnet restore "MerchandiseService/MerchandiseService.csproj"
COPY . .
WORKDIR "/src/MerchandiseService"
RUN dotnet build "MerchandiseService.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "MerchandiseService.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime

WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM runtime AS final
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MerchandiseService.dll"]

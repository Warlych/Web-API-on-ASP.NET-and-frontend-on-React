FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Pharmacy.Presentation/Pharmacy.Presentation.csproj", "Pharmacy.Presentation/"]
RUN dotnet restore "Pharmacy.Presentation/Pharmacy.Presentation.csproj"
COPY . .
WORKDIR "/src/Pharmacy.Presentation"
RUN dotnet build "Pharmacy.Presentation.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Pharmacy.Presentation.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Pharmacy.Presentation.dll"]

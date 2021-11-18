FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DevSecOps-DemoProject/DevSecOps-DemoProject.csproj", "DevSecOps-DemoProject/"]
RUN dotnet restore "DevSecOps-DemoProject/DevSecOps-DemoProject.csproj"
COPY . .
WORKDIR "/src/DevSecOps-DemoProject"
RUN dotnet build "DevSecOps-DemoProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevSecOps-DemoProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevSecOps-DemoProject.dll"]
